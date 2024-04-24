#成功模擬起飛
![image](https://github.com/Pp7887139/my-ros-drone-note/assets/134500400/f8fc0d0d-4e03-4287-b893-7e42fabec8f0)


解決昨天的問題:
AttributeError: module 'em' has no attribute 'RAW_OPT'
[2/729] Generating git version header
ninja: build stopped: subcommand failed.
Makefile:198: recipe for target 'px4_sitl_default' failed
make: *** [px4_sitl_default] Error 1

solve:
刪除版本empy(4版本以上)
pip3 uninstall empy
安裝舊版3系列
pip3 install empy==3.3.4

今日問題:
(1)
Traceback (most recent call last): File “multirotor_communication.py”, line 8, in
from pyquaternion import Quaternion ImportError: No module named pyquaternion

slove:
缺少python pyquaternion物件(按照需要版本py3 or py2 下載)
sudo pip3 install pyquaternion
sudo pip install pyquaternion

(2)
AttributeError: module 'em' has no attribute 'RAW_OPT'
[4/729] Linking CXX static library boards/px4/sitl/src/libdrivers_board.a
ninja: build stopped: subcommand failed.
Makefile:198: recipe for target 'px4_sitl_default' failed
make: *** [px4_sitl_default] Error 1

solve:
empy物件版本問題(4以上容易出現問題)，降為3版本
empy是一種python的模板系統，可以協助處理大量文本，計算模型
pip3 install empy==3.3.4
import em (檢查版本)





 
