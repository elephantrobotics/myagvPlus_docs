# myAGV Plus Isaac Sim 仿真测试手册

**测试环境**：无实车内容，独立台式电脑，NVIDIA RTX 4080 及以上显卡，Isaac Sim 6.0.1，Ubuntu 22.04 + ROS2 Humble。

本手册按控制栈分两章：一、Isaac Sim 自带控制栈；二、ros2_control 路线（真车同款控制栈）。每章内逐项给出启动命令与操作步骤。

**通用前置**（每个新开的终端执行 ROS2 命令前先执行）：

```bash
source /home/elephant/humble_ws/install/setup.bash
```

- Isaac 必须从**已 source 过上面这行的终端**启动（`~/isaacsim/isaac-sim.sh` 或 `ros2 launch isaacsim_bringup ...`），否则找不到本仓库的自定义包（`isaacsim_bringup`、`myagv_plus_navigation2` 等）。

场景文件目录：

```
~/humble_ws/src/myagv_plus_isaac_description/urdf/myagv_plus_isaac_rollers/
```

---

## 一、Isaac Sim 自带控制栈

不接 ros2_control，用 Isaac 自带的 HolonomicController 直接驱动底盘，用于验证麦轮模型、ROS2 桥接、RTX Lidar 本身能不能用。

### 1.1 节点图控制测试（`myagv_plus_isaac_rollers.usda`）

不接 ROS2，用 Isaac 节点图直接给底盘速度，验证麦轮模型本身能不能走。

节点图：

 ![1](..\..\resources\6-SDKDevelopment\6.4/1.png)

**终端 1 —— 启动 Isaac：**

```bash
~/isaacsim/isaac-sim.sh
```

**打开场景**（Isaac 图形界面内操作，不是终端命令）：

GUI 内 `File → Open`，选择双击：

```
~/humble_ws/src/myagv_plus_isaac_description/urdf/myagv_plus_isaac_rollers/myagv_plus_isaac_rollers.usda
```

![2](..\..\resources\6-SDKDevelopment\6.4/2.png)

点击` Don't Save`

![3](..\..\resources\6-SDKDevelopment\6.4/3.png)

**打开控制图：**

`Window → Graph Editors → Action Graph`，选中 `Constant Double3` 节点，在右侧 Property 面板改 `Value`。

![4](..\..\resources\6-SDKDevelopment\6.4/4.png)

![5](..\..\resources\6-SDKDevelopment\6.4/5.png)

![6](..\..\resources\6-SDKDevelopment\6.4/6.png)

**测试：**

点击左侧工具栏 **Play(▶)**，依次修改 `Constant Double3 Node.inputs`（顺序 = `[前进 vx, 横移 vy, 旋转 wz]`）：

| Value | 预期动作 |
|---|---|
| `(0.3, 0, 0)` | 直线前进 |
| `(0, 0.3, 0)` | 横移 |
| `(0, 0, 1.0)` | 原地旋转 |
| `(0, 0, 0)` | 停止 |

---

### 1.2 ROS2 控制测试（`myagv_plus_isaac_rollers_ros2.usda`）

在场景一基础上接入 `/cmd_vel`。

节点图：

 ![7](..\..\resources\6-SDKDevelopment\6.4/7.png)

**终端 1 —— 启动 Isaac：**

```bash
~/isaacsim/isaac-sim.sh
```

**打开场景并 Play**（Isaac 图形界面内操作，不是终端命令）：

`File → Open` 打开：

```
~/humble_ws/src/myagv_plus_isaac_description/urdf/myagv_plus_isaac_rollers/myagv_plus_isaac_rollers_ros2.usda
```

![8](..\..\resources\6-SDKDevelopment\6.4/8.png)

点击 **Play(▶)**。

**终端 2 —— 键盘遥控：**

```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -p stamped:=false
```

必须带 `stamped:=false`——`teleop_twist_keyboard` 默认发布 `TwistStamped`，本节场景的 `ROS2 Subscribe Twist` 节点只收普通 `Twist`，不加这个参数键盘遥控会没反应，模型无法控制位移。

前进/后退 `i`/`,`，转向 `j`/`l`；**按住 `Shift` 横移**，`J`/`L` 左右平移（麦轮特有）。

**预期结果**：`/cmd_vel` 能驱动底盘前进、后退、横移、自转；

---

### 1.3 RTX Lidar 雷达仿真测试（`myagv_plus_isaac_rollers_ros2_lidar.usda`）

在场景 1.2 基础上叠加雷达，产出 `/scan` 与 `/point_cloud`。

节点图：

 ![9](..\..\resources\6-SDKDevelopment\6.4/9.png)

**终端 1 —— 启动 Isaac：**

```bash
~/isaacsim/isaac-sim.sh
```

**打开场景并 Play**（Isaac 图形界面内操作，不是终端命令）：

`File → Open` 打开：

```
~/humble_ws/src/myagv_plus_isaac_description/urdf/myagv_plus_isaac_rollers/myagv_plus_isaac_rollers_ros2_lidar.usda
```

![10](..\..\resources\6-SDKDevelopment\6.4/10.png)

点击 **Play(▶)**。

**终端 2 —— 键盘遥控：**

```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -p stamped:=false
```

前进/后退 `i`/`,`，转向 `j`/`l`；**按住 `Shift` 横移**，`J`/`L` 左右平移（麦轮特有）。

**终端 3 —— 验证 `/scan`：**

```bash
ros2 topic hz /scan 
```

**预期结果**：`/scan` 持续发布，频率接近 10 Hz。键盘遥控移动底盘时，雷达点云随之变化。

![11](..\..\resources\6-SDKDevelopment\6.4/11.png)

---

## 二、ros2_control 路线（真车控制栈）

换成真车控制栈 `controller_manager` + `mecanum_drive_controller`，仿真中标定的参数可直接用于真车。

### 2.1 ros2_control 控制链测试（`myagv_plus_isaac_rollers_sim.usda`）

`/cmd_vel` 改为 `TwistStamped`；`/odom` 由轮速正解得出，麦轮打滑会真实漂移，和真车表现一致（非缺陷）。

**终端 1 —— 启动 Isaac、载入场景并自动 Play：**

```bash
ros2 launch isaacsim_bringup run_isaacsim.launch.py play_sim_on_start:=true \
  gui:=$HOME/humble_ws/src/myagv_plus_isaac_description/urdf/myagv_plus_isaac_rollers/myagv_plus_isaac_rollers_sim.usda
```

**终端 2 —— 确认 `/clock` 持续输出后，启动控制栈 + RViz：**

```bash
ros2 topic hz /clock
# 看到持续输出后按 Ctrl+C，再执行：
ros2 launch isaacsim_bringup sim_bringup.launch.py use_rviz:=true
```

**终端 3 —— 键盘遥控（`/cmd_vel` 为 `TwistStamped`）：**

```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

![12](..\..\resources\6-SDKDevelopment\6.4/12.png)

**预期结果**：键盘遥控移动底盘时，雷达点云随之变化。

---

### 2.2 仿真建图测试

四套官方场景任选其一，文件都在 `~/isaacsim/scenes/`：

| 场景 | 文件名 |
|---|---|
| 简仓 | `myagv_plus_warehouse.usda` |
| 多货架 | `myagv_plus_multiple_shelves.usda` |
| 大仓 | `myagv_plus_full_warehouse.usda` |
| 办公室 | `myagv_plus_office.usda` |

以下以多货架场景为例，所有终端需先执行前面的「通用前置」。

**终端 1 —— 启动 Isaac、载入场景并自动 Play：**

```bash
ros2 launch isaacsim_bringup run_isaacsim.launch.py \
  gui:=$HOME/isaacsim/scenes/myagv_plus_multiple_shelves.usda \
  play_sim_on_start:=true
```

**终端 2 —— 确认 `/clock` 持续输出后，启动 ros2_control 底盘：**

```bash
ros2 topic hz /clock
# 看到持续输出后按 Ctrl+C，再执行：
ros2 launch isaacsim_bringup sim_bringup.launch.py use_rviz:=false
```

**终端 3 —— 启动 gmapping：**

```bash
ros2 launch slam_gmapping slam_gmapping.launch.py use_sim_time:=true
```

**终端 4 —— 键盘遥控采集：**

```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

低速平移和旋转，扫完整个场景边界及货架通道，最后回到建图起点附近形成回环，RViz 中地图稳定后再存图。

**终端 5 —— 保存地图：**

```bash
ros2 run nav2_map_server map_saver_cli \
  -f ~/humble_ws/src/myagv_plus_navigation2/map/map \
  --ros-args -p use_sim_time:=true
```

**预期结果**：`map.pgm` / `map.yaml` 落盘于 `myagv_plus_navigation2/map/`，RViz 中地图形状与场景吻合；

![13](..\..\resources\6-SDKDevelopment\6.4/13.png)

---

### 2.3 仿真导航测试

基于「2.2 仿真建图测试」保存的地图，场景需与建图时使用的一致。

**终端 1 —— 启动 Isaac、载入场景并自动 Play：**

```bash
ros2 launch isaacsim_bringup run_isaacsim.launch.py \
  gui:=$HOME/isaacsim/scenes/myagv_plus_multiple_shelves.usda \
  play_sim_on_start:=true
```

**终端 2 —— 确认 `/clock` 持续输出后，启动控制栈（不起 RViz）：**

```bash
ros2 topic hz /clock
# 看到持续输出后按 Ctrl+C，再执行：
ros2 launch isaacsim_bringup sim_bringup.launch.py use_rviz:=false
```

**终端 3 —— 启动导航：**

```bash
ros2 launch myagv_plus_navigation2 navigation2_active.launch.py use_sim_time:=true
```

**RViz 操作：**

1. **2D Pose Estimate**：在地图上点击小车实际所在位姿（建图起点附近），等 AMCL 粒子云收敛、`map → odom` 对齐。不给初始位姿无法定位。
2. **Nav2 Goal**：在空地点击目标点，观察小车规划路径并前往。

**预期结果**：定位成功，激光与地图基本重合；能下发目标点并规划路径到达，遇到障碍物能绕行。

![14](..\..\resources\6-SDKDevelopment\6.4/14.png)
