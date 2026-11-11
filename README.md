# omron_gripper_capabilities

Omron-specific plans, configuration, system launch, and providers for the soft two-finger gripper. The reusable runner implementations and base interfaces are owned by [gripper_capabilities](../gripper_capabilities).

## Supported runners

| Runner | Description |
| --- | --- |
| `OmronGripperLaunchRunner` | Starts the gripper stack and waits for `/gripper_command`. |
| `OmronGripperCommandRunner` | Sends a `control_msgs/action/GripperCommand` goal with target `position` and optional `max_effort`. |
| `OmronGripperStateRunner` | Reads the current gripper articulation and emits `joint_names` plus `joint_positions` vectors. |

For interface details, see [docs/interface.md](./docs/interface.md).

## Example Plans

- [plans/gripper_1.xml](./plans/gripper_1.xml): open, close by position control, then open again.
- [plans/gripper_2.xml](./plans/gripper_2.xml): open, close with explicit `max_effort`, then open again.

The example plans use `position="0.08"` for open and `position="0.0"` for closed. Adjust those values if your active gripper driver uses a different travel range.

The example plans use `position="0.08"` for open and `position="0.0"` for closed. Adjust these values if the deployed gripper has a different travel range.

## Build

```bash
cd ~/colcon_ws
colcon build --packages-up-to omron_gripper_capabilities --symlink-install
```

## Runtime

Start the active gripper action server, then run one of the gripper plans through the packaged wrapper launch.

```bash
source install/setup.bash
ros2 launch omron_gripper_capabilities system.launch.py filename:=gripper_1.xml
```

The wrapper starts Fabric, Capabilities2, and prompt tools automatically. Add `start_prompt_tools:=false` when you want to exclude `prompt_bridge`. Experience is integrated into Fabric, and supervisor functionality is provided by the relevant packages; there is no separate Experience/Supervisor launch flag.# omron_gripper_capabilities
