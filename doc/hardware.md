## Main Components
1. A component that detect the line of sight of the fursuiter.
   一个检测兽装穿戴者视线方向（眼睛指向方向）的组件
2. A component that detect the facial expression of the fursuiter.
   一个检测兽装穿戴者面部表情的组件
3. A component that record/ detect the persons (physical movement (or facial expression as well)) in front of the fursuit (the person that interact with the fursuit). Should also be able to detect whether there are people in front of the fursuit and the environment brightness level.
   一个检测兽装前方互动者的动作（或者包含面部表情）的组件。应该同时能检测兽装前方是否有观众，以及当前环境光的亮度。
   Remark: I doubt if we should detect facial expression as well. It will require higher definition camera, which will consume more energy, and analyzing facial expression contribute little to the control program.
5. A Central Control Unit (CCU)
   Should recieve status and parameters from all other detection components, and send control command to LED display component. Should also be able to connect to external device to adjust configurable parameters (including
    but not limited to fine tuning the sync and interact effects, adjusting reaction speed and power consumption preset), toggle functions, and uploading new display pictures or animations.
   一个中央控制单元，负责接受检测组件的状态和传入的参数，并向LED显示设备发射控制命令。应该同时具有连接外部设备的功能，通过外部设备调节配置参数（包括但不限于调整LED显示的同步和互动效果，调节响应速度，调节能耗预设），开关某一功能，上传新的动画和图片
6. An LED Display Component
   LED显示设备

## Harware Design Principles
- Topological Structure: Layered Hybrid Architecture
    1. Each input components should only report status and concise parameters to CCU. That means they should process the data inside their own unit, and generate a set of enum type parameter (or perhaps a number type parameter) to CCU to describe their input.
    Furthermore, CCU should only use a set of enum type (or number type) parameters to command the LED display to transition to designated animations/pictures. This design should ease CCU from having to process massive data and telling LED light up which pixels.
    Letting each components handle its own functions and datas should results in higher efficiency, since we can put processing unit optimized for certain function into each components. (General-purpose processing unit used in CCU is low-efficient)
    2. To achieve such design, a central power supply/control unit should also be included. It should be seperated from CCU to improve safety and reduce signal noise.
  拓扑结构：分层混合架构
      1. 每个输入部件应该仅仅向中央控制单元发送状态和简洁的参数。所以他们应该在自己部件内部处理好数据，并且生成一系列枚举类型的参数（或者一些数字类型的参数）给中央处理单元，来描述他们接收到的输入。
         中央控制单元应该仅仅向LED显示部件发送一系列枚举类型的参数（或者一些数字类型的参数），来控制LED显示部件切换动画和图片。这样的设计应该能够使得中央控制单元不需要处理大量的数据，并且每次都将要显示什么样的图片的指令发送给LED显示屏。
- LED Display Requirement Analysis:
    1. Fursuiter should be able to see through the LED display.
    2. LED display equipment should have at least two power preset---Idle and Active. When fursuiter are not active or the camera detects no audience in front of the suit, the display will be in Idle preset. The eye pattern is static and the backlight is set to minimum level or off. In Active mode, the display will be set to highest refresh rate and adjust backlight accroding to the environment birghtness.
    3. A small question: is it possible for an LED display to show a specific pattern even when the entire system is completely powered off — for example, the last frame before shutdown — by using a non-backlit state to make it visible?
      Or alternatively, could the LED panel itself be coated with a fixed pattern that becomes visible when the screen is completely black, but is normally hidden when the LEDs are lit?
  LED显示屏需求分析：
    1.兽装穿戴者应该能够透过屏幕看到外界。
    2.LED显示设备应该具有至少两个电源预设——待机与激活。当兽装穿戴者不活跃或者镜头检测到前方并没有观众时，显示屏应该进入待机设定。此时，眼睛的图案应该是静止不动并且背光应该处于最低或者完全关闭。在激活设定下，屏幕应该处于最大刷新率且屏幕亮度应该能跟随环境光亮度来调节。
    3.一个小问题：我们是否可以让LED屏在整个系统完全不上电时都能显示某一个特定的图案，比如是关机前的最后一个画面，通过无背光状态来显示。或者就是LED屏幕上单纯涂了一个图案，当LED屏幕全黑时就能显现出来被看到，平时会被LED的显示盖过去。
## Topological Structure
