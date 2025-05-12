// delivery_node.cpp

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"
#include "sensor_msgs/msg/nav_sat_fix.hpp"
#include "geographic_msgs/msg/geo_pose_stamped.hpp"
#include "mavros_msgs/srv/command_bool.hpp"
#include "mavros_msgs/srv/command_tol.hpp"
#include "mavros_msgs/msg/state.hpp"

using std::placeholders::_1;

enum class MissionStatus {
  IDLE,
  TAKEOFF,
  ENROUTE,
  LANDING,
  RETURNING,
  COMPLETED
};

class DeliveryNode : public rclcpp::Node {
public:
  DeliveryNode() : Node("delivery_node") {
    status_pub_ = this->create_publisher<std_msgs::msg::String>("/delivery_status", 10);
    goal_sub_ = this->create_subscription<geographic_msgs::msg::GeoPoseStamped>(
      "/delivery_goal", 10, std::bind(&DeliveryNode::goal_callback, this, _1));
    gps_sub_ = this->create_subscription<sensor_msgs::msg::NavSatFix>(
      "/mavros/global_position/global", 10, std::bind(&DeliveryNode::gps_callback, this, _1));

    set_status(MissionStatus::IDLE);
  }

private:
  rclcpp::Publisher<std_msgs::msg::String>::SharedPtr status_pub_;
  rclcpp::Subscription<geographic_msgs::msg::GeoPoseStamped>::SharedPtr goal_sub_;
  rclcpp::Subscription<sensor_msgs::msg::NavSatFix>::SharedPtr gps_sub_;

  geographic_msgs::msg::GeoPoseStamped target_;
  sensor_msgs::msg::NavSatFix current_pos_;
  geographic_msgs::msg::GeoPoseStamped home_;
  MissionStatus status_;

  void goal_callback(const geographic_msgs::msg::GeoPoseStamped::SharedPtr msg) {
    target_ = *msg;
    home_.pose.position.latitude = current_pos_.latitude;
    home_.pose.position.longitude = current_pos_.longitude;
    home_.pose.position.altitude = current_pos_.altitude;

    set_status(MissionStatus::TAKEOFF);
    execute_mission();
  }

  void gps_callback(const sensor_msgs::msg::NavSatFix::SharedPtr msg) {
    current_pos_ = *msg;
  }

  void execute_mission() {
    if (status_ == MissionStatus::TAKEOFF) {
      RCLCPP_INFO(this->get_logger(), "Taking off...");
      // TODO: call arm service & takeoff
      set_status(MissionStatus::ENROUTE);
      // TODO: publish target setpoint
    } else if (status_ == MissionStatus::ENROUTE) {
      // Check distance to target, then LAND
      set_status(MissionStatus::LANDING);
    } else if (status_ == MissionStatus::LANDING) {
      RCLCPP_INFO(this->get_logger(), "Landing...");
      // TODO: call land service
      set_status(MissionStatus::RETURNING);
    } else if (status_ == MissionStatus::RETURNING) {
      RCLCPP_INFO(this->get_logger(), "Returning to launch...");
      // TODO: takeoff again and publish home_ setpoint
      set_status(MissionStatus::COMPLETED);
    } else if (status_ == MissionStatus::COMPLETED) {
      RCLCPP_INFO(this->get_logger(), "Mission completed. Disarming.");
      // TODO: call disarm service
    }
  }

  void set_status(MissionStatus new_status) {
    status_ = new_status;
    auto msg = std_msgs::msg::String();
    msg.data = status_to_string(status_);
    status_pub_->publish(msg);
  }

  std::string status_to_string(MissionStatus status) {
    switch (status) {
      case MissionStatus::IDLE: return "IDLE";
      case MissionStatus::TAKEOFF: return "TAKEOFF";
      case MissionStatus::ENROUTE: return "ENROUTE";
      case MissionStatus::LANDING: return "LANDING";
      case MissionStatus::RETURNING: return "RETURNING";
      case MissionStatus::COMPLETED: return "COMPLETED";
      default: return "UNKNOWN";
    }
  }
};

int main(int argc, char * argv[]) {
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<DeliveryNode>());
  rclcpp::shutdown();
  return 0;
}
