
### Prerequisites

Make sure you have `ros2` already installed on your system

### Setup

#### Download and install foxglove-studio on your platform

follow the instructions provided by foxglove here [foxglove download instructions](https://foxglove.dev/download)

#### Download and install foxglove_bridge

**foxglove_bridge** is used to transfer real time data to foxglove studio via the Foxglove Websocket Connection (default port 8765) follow the link for a detailed installation instruction [foxglove_bridge installation](https://docs.foxglove.dev/docs/connecting-to-data/ros-foxglove-bridge)

When launched via the `ros2 launch foxglove_bridge foxglove_bridge_launch.xml`  command a new ros node is started. This node must run on the same network as the other nodes e.g. the robot itself in order to listen in on the published topics.

##### Optional

###### Ensure startup of foxglove_bridge

It is advised to add foxglove_bridge to the launch file in order to ensure the initialization of the data transfer anytime the ros network is online.

Example configuration
```python
### Launch configuration variables specific to simulation
use_foxglove_bridge = LaunchConfiguration('use_foxglove_bridge')

### Declare the launch arguments
declare_use_foxglove_bridge = DeclareLaunchArgument(
name='use_foxglove_bridge',
default_value='True',
description='Wether to start an additional foxglove_bridge ROS node for live data streaming')

### Launch Foxglove Bridge
start_foxglove_bridge = Node(
condition=IfCondition(use_foxglove_bridge),
package='foxglove_bridge',
executable='foxglove_bridge',
name='foxglove_bridge'
# arguments=[''] # Left empty on purpose
)

### Declare the launch options and add actions
ld.add_action(declare_use_foxglove_bridge)
ld.add_action(start_foxglove_bridge)
```

###### Further Configuration

foxglove_bridge can be configured by setting one or more of the following parameters at initialization. Either through a launch file or by passing them as cli arguments.

A List of all relevant configuration parameters and their default values.

- `port: Default is 8765.`
- `address: Default is 0.0.0.0.`
- `tls: Default is false.`
- `certfile: Default is "".`
- `keyfile: Default is "".`
- `topic_whitelist: Default is ["*"].`
- `service_whitelist: Default is ["*"].`
- `param_whitelist: Default is ["*"].`
- `client_topic_whitelist: Default is ["*"].`
- `send_buffer_limit: Default is 10000000 (10 MB).`
- `use_compression: Not specified, boolean value.`
- `capabilities: Default is [clientPublish, parameters, parametersSubscribe, services, connectionGraph, assets].`
- `asset_uri_allowlist: Default is ["^package://(?:\w+/)*\w+\.(?:dae|fbx|glb|gltf|jpeg|jpg|mtl|obj|png|stl|tif|tiff|urdf|webp|xacro)$"].`
- `num_threads: Default is 0`
- `min_qos_depth: Default is 1`
- `max_qos_depth: Default is 25`
- `include_hidden: Default is false`

refer to [foxglove_bridge installation](https://docs.foxglove.dev/docs/connecting-to-data/ros-foxglove-bridge) for a detailed description of their uses

### Capturing Live Data with Foxglove Studio

#### Run your **ros** package.

If you haven't added fox_bridge to your **launch** file you can start the foxglove bridge node the following way:

`ros2 run foxglove_bridge foxglove_bridge`

#### Start the Foxglove Studio Application

On the dashboard select 
`Open connection...` 

Leave the default WebSocket URL as is `ws://localhost:8765`unless the port was configured otherwise

#### Verify the connection to your robot

In the top left corner click on `Add panel` and select `Topic Graph`

You should now see a graph with all your active Ros nodes.

**To remove a panel**, klick on the three dots in the top right of a panel and select `remove panel`


