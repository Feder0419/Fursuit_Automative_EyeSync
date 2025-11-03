## Main Components
1. A component that detect the line of sight of the fursuiter.
   一个检测兽装穿戴者视线方向（眼睛指向方向）的组件
2. A component that detect the facial expression of the fursuiter.
   一个检测兽装穿戴者面部表情的组件
3. A component that record/ detect the persons (physical movement (or facial expression as well)) in front of the fursuit (the person that interact with the fursuit).
   一个检测兽装前方互动者的动作（或者包含面部表情）的组件
   Remark: I doubt if we should detect facial expression as well. It will require higher definition camera, which will consume more energy, and analyzing facial expression contribute little to the control program.
5. A Central Control Unit (CCU)
   Should recieve status and parameters from all other detection components, and send control command to LED display component. Should also be able to connect to external device to adjust configurable parameters (including
    but not limited to fine tuning the sync and interact effects, adjusting reaction speed and power consumption preset), toggle functions, and uploading new display pictures or animations.
   一个中央控制单源，负责接受检测组件的状态和传入的参数，并向LED显示设备发射控制命令。应该同时具有连接外部设备的功能，通过外部设备调节配置参数（包括但不限于调整LED显示的同步和互动效果，调节响应速度，调节能耗预设），开关某一功能，上传新的动画和图片
6. An LED Display Component
   LED显示设备

## Harware Design Principles
- Topological Structure: Layered Hybrid Architecture
    1. Each input components should only report status and concise parameters to CCU. That means they should process the data inside their own unit, and generate a set of enum type parameter (or perhaps a number type parameter) to CCU to describe their input.
    Furthermore, CCU should only use a set of enum type (or number type) parameters to command the LED display to transition to designated animations/pictures. This design should ease CCU from having to process massive data and telling LED light up which pixels.
    Letting each components handle its own functions and datas should results in higher efficiency, since we can put processing unit optimized for certain function into each components. (General-purpose processing unit used in CCU is low-efficient)
    2. To achieve such design, a central power supply/control unit should also be included. It should be seperated from CCU to improve safety and reduce signal noise.
- LED Display Requirement Analysis://TODO
  Two power preset design. Should be able to see through the display.

## Topological Structure
