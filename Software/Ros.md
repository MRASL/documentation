> **Info** Since there is an astounding amount of information out there, for now we copy the page https://github.com/ethz-asl/ros_best_practices/wiki into our own documentation. The best way to learn ROS is probably to start with official tutorials.

# ROS Best Practices

This is a loose collection of best practices, conventions, and tricks for using the Robot Operating System ([ROS]). It builds up on the official ROS documentation and other resources and is meant as summary and overview.

Official ROS documentation:

* [ROS Enhancement Proposals (REPs)](http://www.ros.org/reps/rep-0000.html),
* [ROS Use Patterns and Best Practices](http://wiki.ros.org/ROS/Patterns),
* [ROS Developer’s Guide](http://wiki.ros.org/DevelopersGuide).

Other References:

* [Programming for Robotics - Introduction to ROS: Péter Fankhauser, ETH Zürich, March 2017](https://www.researchgate.net/publication/314101187_Programming_for_Robotics_-_Introduction_to_ROS),
* [ROS Best Practices: Lorenz Mösenlechner, Technische Universität München, July 2012](http://robohow.eu/_media/meetings/first-integration-workshop/ros-best-practices.pdf),
* [ROS Best Practices: Tully Foote, Open Source Robotics Foundation, October 2014](http://nerve.uml.edu/ros-2014/ROS%20Best%20Practices%20-%20Tully%20Foote.pdf),
* [ROS Design Patterns, C++ APIs, and Best Practices: Jonathan Bohren, Laboratory for Computational Sensing and Robotics, The John Hopkins University](https://courses.cs.washington.edu/courses/cse466/11au/calendar/ros_cc_2_patterns.pdf),
* [ROS Answers](http://answers.ros.org/questions/scope:all/sort:activity-desc/tags:best_practices/).

In parts, the document describes opinionated best practices established within the Legged Robotics Group from the Autonomous Systems Lab, ETH Zurich.

**Author: Péter Fankhauser, pfankhauser@ethz.ch<br />
Affiliation: Autonomous Systems Lab, ETH Zurich**

## TODO

* http://robotics.stackexchange.com/questions/3110/ros-best-practices

## Before You Begin

Research other products out there already: [http://www.ros.org/browse/list.php](http://www.ros.org/browse/list.php)

## Coding Guidelines

Refer to the [ROS C++ Style Guide](http://wiki.ros.org/CppStyleGuide). At the Autonomous Systems Lab we use the [Google style-guide](https://github.com/ethz-asl/programming_guidelines/wiki/Cpp-Coding-Style-Guidelines).

## Units and Coordinate Conventions

Refer to [Standard Units of Measure and Coordinate Conventions](http://www.ros.org/reps/rep-0103.html).

## Coordinate Frames

* [Coordinate Frames for Mobile Platforms](http://www.ros.org/reps/rep-0105.html)
* [Coordinate Frames for Humanoids Robots](http://www.ros.org/reps/rep-0120.html)

## Testing

Refer to [http://wiki.ros.org/UnitTesting](http://wiki.ros.org/UnitTesting).

## Package Organization

- The overhead of a ROS package is not large. Define separate packages wherever they make sense. Often, code can be useful in contexts other than those for which it was built.
- Avoid combining nodes that pull in mutually unneeded dependencies and are often used separately (to eliminate unnecessary build overhead).
- The package dependency graph must be acyclic, i.e. no package may depend on another that directly or indirectly depends on it.
- If programs with similar dependencies are generally used together, consider combining them into a single package.
- If some nodes have common dependencies on shared code that you do not wish to export publicly, they can be combined internally within a single package.
- **Create separate packages that contain only messages, services and actions (separation of interface and implementation).** Examples for separate message packages are the [ros/common_msgs](https://github.com/ros/common_msgs) packages.
- Group packages in stacks.

Sources:

- [When should I split my code into multiple packages, and what’s a good way to split it?](http://answers.ros.org/question/11835/when-should-i-split-my-code-into-multiple-packages-and-whats-a-good-way-to-split-it/)
- [Packages vs nodes](http://answers.ros.org/question/9133/packages-vs-nodes/)

References:

- [Metapackages](http://wiki.ros.org/Metapackages)

## Package Naming

Refer to [Naming ROS Resources](http://wiki.ros.org/ROS/Patterns/Conventions) and [REP-144: ROS Package Naming](https://github.com/ros-infrastructure/rep/blob/master/rep-0144.rst) (draft).

Choose the name carefully:

- They are messy to change later.
- Package names are global to the entire ROS ecosystem.
- Try to pick names that will make sense to others who may wish to use your code.
- Package names should be specific enough to identify what the package does. Do not over scope, e.g. *planner* is a bad name, use *wavefront_planner* instead.
- Do not use “utils” or other catchalls.
- Prefixing a package name is recommended ***only*** when the package is not meant to be used more widely (e.g., packages that are specific to the StlarETH robot use the ‘starleth_’ prefix).

## Naming Conventions for Packages, Nodes, Topics, Services, TF etc.

Adapted from [ROS Best Practices: Lorenz Mösenlechner, Technische Universität München, July 2012](http://robohow.eu/_media/meetings/first-integration-workshop/ros-best-practices.pdf):

- Package names are lower case.
- Packages must not contain dashes (“-”), only underscores (“_”).
- Nodes, topics, services, actions, parameters are all lower case with underscores as separator.
- Messages, services and actions are named in camel case: `geometry_msgs/PoseStamped`.
- Names in a message/service/action definition are all lower case with underscores as separator: `geometry_msgs/Pose end_effector`.
- Do not use the word “action” in an action definition: `Foo.action`, not `FooAction.action`.

## Custom ROS Message and Services

- **Use standard data types whenever possible (try to prevent `.msg` proliferation)!** For example, instead of creating a custom `EstimatorUpdateTime.msg`, use the [`std_msgs/Time.msg`](http://docs.ros.org/api/std_msgs/html/msg/Time.html) definition. Another example is an empty service call `TriggerComputation.msg`, use [`std_srvs/Empty.srv`] (http://docs.ros.org/api/std_srvs/html/srv/Empty.html) instead.
- **Do not define a new msg/srv/action definition for each topic/service/action!** For example, instead of creating two  definitions `LoadMapFromFile.srv` and `SaveMapToFile.srv` with the same content

		string file_path
		—

	define one type ‘ProcessFile.srv’ which can be used from both services, `~/load_map` and `~/save_map`, respectively.
- Complex messages are built through composition (e.g. [`geometry_msgs/PoseWithCovarianceStamped`](http://docs.ros.org/api/geometry_msgs/html/msg/PoseWithCovarianceStamped.html)).
- Try to avoid building messages that tend to not get completely filled out.

References:

- [std_msgs](http://wiki.ros.org/std_msgs)
- [common_msgs](http://wiki.ros.org/common_msgs)


## Documentation

- Create a short README.md/Wiki for each package:
	- Document what the node does,
	- Document topics, services and actions that are required and provided,
	- Document ROS parameters and their default values,
	A template for the `README.md` is provided [here](https://github.com/ethz-asl/ros_best_practices/blob/master/ros_package_template/README.md)
- Provide launch files,
- Provide a rosinstall file.

## File/Folder Structure for Packages

Use this file/folder structure for a general ROS package:

	package_name
	|— config
		|— robots
			|— my_robot.yaml
		|— sensors
			|— velodyne.yaml
			|— hokuyo_laser_range.yaml
	|— include/package_name
		|— Class1.hpp
		|— Class2.hpp
	|— launch
		|— node1_name.launch
		|— node2_name.launch
	|— rviz
		|— package_name.rviz
	|— scripts
		|— my_script.py
	|— src
		|— Class1.cpp
		|— Class2.cpp
		|— node1_name_node.cpp
		|— node2_name_node.cpp
	|— test
		|— Class1Test.cpp
		|— Class2Test.cpp
		|— test_package_name.cpp
	|— CMakeLists.txt
	|— package.xml

For ROS message and service definitions use:

	package_name_msgs
	|— action
		|— MyAction.action
	|— msg
		|— MyMessage.msg
	|— srv
		|— MyService.srv
	|— CMakeLists.txt
	|— package.xml

References:

* [Packages: Common_Files_and_Directories](http://wiki.ros.org/Packages#Common_Files_and_Directories)

## Topics vs Services vs Actionlib vs Parameters vs Dynamic Parameters

Refer to [ROS Patterns - Communication](http://wiki.ros.org/ROS/Patterns/Communication#Topics_vs_Services_vs_Actionlib…).

Summary:

- Use topics for publishing continuous streams of data, e.g. sensor data, continuous detection results, …
- Use services only for short calculations.
- Use actions for all longer running processes, e.g. grasping, navigation, perception, …
- Use parameters for values which are known at launch and are not likely to change during run time.
- Use dynamic parameters (`dynamic_reconfigure`) for parameter which are likely to change during run time.

## Publishing Spatial / Geometric Data

Refer to [http://wiki.ros.org/ROS/Patterns/Communication](http://wiki.ros.org/ROS/Patterns/Communication#Publishing_Spatial_.2BAC8_Geometric_Data).

## Node Handles
There are four main types of node handles:

1. **Default (public) node handle: `nh_ = ros::NodeHandle();`**
2. **Private node handle: `nh_private_ = ros::NodeHandle(“~”);`**
3. Namespaced node handle: `nh_aslam_ = ros::NodeHandle(“aslam”);`
4. Global node handle: `nh_global_ = ros::NodeHandle(“/“);` (You probably shouldn’t use this ever.)

Generally you will only use the first 2 -- you could also use the namespaced node handle for separating out publishers for nodes that have many.

To explain what these do and how they should be used, let’s assume your ROS node is named `ros_node`, in namespace `blah`, and you are trying to look up the name `topic`. Here is what they will resolve to using all 4 node handles:

1. `/blah/topic`
2. `/blah/ros_node/topic`
3. `/blah/aslam/topic`
4. `/topic`

If, instead, your try to resolve `/topic`, this will skip the namespace of the node and resolve to `/topic`.

## When to Use Which Node Handle
These are just general guidelines, but when possible, prefer to use the following in each case:

* **Subscribers** - usually public node handles.
* **Publishers** - usually private node handles for most output/visualization, occasionally necessary to use public for globally-used data (i.e., `/odom` topic).
* **Parameters** - almost always private node handle.

**Never use global names.** This is because they do not resolve properly when you push nodes into namespaces, and does not allow you to run more than one of your node at a time properly. Or use multiple robots on the same master. Define published topics and parameters relative to the nodes namespace:

**Good**: `odometry`, `grid_map`, `cam0/camera_info`  
**Bad**: `/odometry`, `/grid_map`, `/helicopter/cam0/camera_info`

## Topic Naming

Topics should be named in the context of the node. Very simple and clear names are preferred for a easy to understand “ROS API”. Topic names not cause collision as long as they are published within the namespace of the node (see *Namespace for Topics and Parameters*).

In order to tell another node where to subscribe, set the topic name as ROS parameter (preferred). Alternatively, for third-party nodes, you can use the [`remap`](http://wiki.ros.org/roslaunch/XML/remap) tag in roslaunch.

References:

* [When Topics Should be Remapped](http://wiki.ros.org/ROS/Patterns/Communication#When_Topics_Should_be_Remapped)
* [Remapping Arguments](http://wiki.ros.org/Remapping%20Arguments)

## Parameter Naming

Use a hierarchical scheme for parameters, such as

	camera/left/name: left_camera
	camera/left/exposure: 1
	camera/right/name: right_camera
	camera/right/exposure: 1.1

instead of

	camera_left_name: left_camera

etc. This protects parameter names from colliding and allows parameters to be access individually or as a tree. In a YAML-file, the structure would be

	camera:
	  left:
	    name: left_camera
	    exposure: 1
	  right:
	    name: right_camera
	    exposure: 1.1

References:

* [Parameter Server](http://wiki.ros.org/Parameter%20Server)

## Parameter Organisation

If your node has only one or two parameters, you can set them in a launch file with the `<param>` tag:

	<launch>
		<node pkg="my_package" type="my_node" name="my_name" output="screen">
			<param name="my_parameter" value="10" />
		</node>
	</launch>

In general (preferred), organize the parameters in YAML-files and load them via the `rosparam`-tag:

	<launch>
 		<node pkg="my_package" type="my_node" name="my_name" output="screen">
			<rosparam command="load" file="$(find my_package)/config/robots/starleth.yaml" />
    		<rosparam command="load" file="$(find my_package)/config/sensors/default.yaml" />
 		</node>
	</launch>

Do not use command line parameters but the ROS parameter server. For parameters that are likely to change at runtime, use [dynamic_reconfigure](http://wiki.ros.org/dynamic_reconfigure).

References:

* [ROS Patterns / Parameterization](http://wiki.ros.org/ROS/Patterns/Parameterization)
* [roslaunch / XML](http://wiki.ros.org/roslaunch/XML#Setting_parameters)
* [\<rosparam\> tag](http://wiki.ros.org/roslaunch/XML/rosparam)

## Using Third-Party Libraries

Encourages standalone libraries with no ROS dependencies. Don’t put ROS dependencies in the core of your algorithm!

If you can develop a ROS independent library and release a parallel ROS wrapper

http://courses.csail.mit.edu/6.141/spring2012/pub/lectures/Lec06-ROS.pdf

Refer to [Using Third-Party Libraries](http://wiki.ros.org/UsingThirdPartyLibraries).

- If possible, try to use libraries from Debian packages.
- Specify rosdep dependencies (tool for installing system packages).
- If you need to compile a library from source create a ROS wrapper package that downloads and compiles the package.
- Don’t use sudo in wrapper packages.
- Don’t require manual system wide installations.
- Don’t copy libraries into packages that need them.

## Building

Never call cmake by hand in a package.

## Dependencies

Keep your dependencies clean:

- Only depend on what you need,
- Specify all dependencies,
- Do not use implicit dependencies.

**If multiple runs of `catkin_make` are required for your workspace to be built, something is fishy!**

## Startup Order

Do not require a specific startup order for nodes. Use `waitForService`, `waitForTransform`, `waitForServer`, …

## Roslaunch Organization

Refer to [Roslaunch tips for large projects](http://wiki.ros.org/roslaunch/Tutorials/Roslaunch%20tips%20for%20larger%20projects).

	<include file=“$(find package_name)/launch/another.launch”/>

## Printing Messages/Logging

- Use rosconsole utilities for logging(`ROS_INFO`,`ROS_DEBUG`, …).
- Use appropriate console logging: Debug, info, warn, error, fatal.
- Provide introspection/debug topics.

## Debugging

TODO.

## Checking the Number of Subscribers

To avoid computational overhead for topics which no nodes are subscribed to, check the number of subscribers with

	if (publisher.getNumSubscribers() < 1) return;

## ROS Bag Files

* Recording of a bag:

		rosbag record <topic> <topic> …

* Play a bag:

		rosbag play foo.bag

* Play a bag using recorded time (important when stamped data and TF was recorded):

		rosbag play --clock foo.bag

	Note: The `/use_sim_time` parameter must be set to true before the node is initialized.

		rosparam set use_sim_time true

References:

* [Clock](http://wiki.ros.org/Clock)

## Time

Use `ros::Time`, `ros::Duration`, and `ros::Rate` instead of system time.

## Converting Between ROS Messages and Other Types

### Eigen

To convert to/from messages, use **[eigen_conversions](http://wiki.ros.org/eigen_conversions)** (or [kindr-](https://github.com/ethz-asl/kindr/tree/master/include/kindr/thirdparty/ros) or [minkindr-conversions](https://github.com/ethz-asl/minkindr_ros)).

Example:

	Eigen::Vector3d my_super_cool_vector(1.0, 2.0, 3.0);
	geometry_msgs::Point point_msg;
	tf::pointEigenToMsg(my_super_cool_vector, point_msg);
	super_cool_publisher_.publish(point_msg);

To go to/from TF, use **[tf_conversions](http://wiki.ros.org/tf_conversions)** (or also [kindr-](https://github.com/ethz-asl/kindr/tree/master/include/kindr/thirdparty/ros) or [minkindr-conversions](https://github.com/ethz-asl/minkindr_ros)).

Example:

	Eigen::Vector3d my_super_cool_vector(1.0, 2.0, 3.0);
	tf::Vector3 my_super_cool_vector_tf;
	tf::vectorEigenToTF(my_super_cool_vector, my_super_cool_vector_tf);
	tf::Transform transform;
	transform.setOrigin(my_super_cool_vector_tf);
	transform_broadcaster_.sendTransform(
		tf::StampedTransform(transform, ros::Time::now(), “map”, “world”));

References:

* [Eigen Conversions](http://docs.ros.org/indigo/api/eigen_conversions/html/namespacetf.html)
* [TF Conversions](http://docs.ros.org/indigo/api/tf_conversions/html/c++/tf__eigen_8h.html)

### OpenCV Image

Use the **[cv_bridge](http://wiki.ros.org/cv_bridge)**. This allows very easy conversions to/from ROS messages.

Example:

	const stereo_msgs::DisparityImageConstPtr& msg;  // We got this from a subscription callback.
	cv::Mat output_image;
	cv_bridge::CvImageConstPtr cv_img_ptr = cv_bridge::toCvShare(msg->image, msg);
	// This is a shallow copy.
	output_image = cv_img_ptr->image;

	cv_bridge::CvImage image_cv_bridge;
	image_cv_bridge.header.frame_id = “map”;
	image_cv_bridge.image = output_image;
	publisher_.publish(image_cv_bridge.toImageMsg());

References:

* [ROS Tutorial](http://wiki.ros.org/cv_bridge/Tutorials/UsingCvBridgeToConvertBetweenROSImagesAndOpenCVImages)
* [cv_bridge Documentation](http://docs.ros.org/indigo/api/cv_bridge/html/c++/classcv__bridge_1_1CvImage.html)

## Catkin Build Flags

These are some useful CMake flags for catkin. To use them with [catkin_tools](http://catkin-tools.readthedocs.io/en/latest/verbs/catkin_config.html), add them as arguments with

	catkin config [list of your flags]

So for example

	catkin config -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_COMPILER_ARG1=-std=c++11

Useful catkin build flags:

* Build in C++ release mode

		-DCMAKE_BUILD_TYPE=Release

* Build with C++11

		-DCMAKE_CXX_COMPILER_ARG1=-std=c++11

* Build Eclipse projects

		-G"Eclipse CDT4 - Unix Makefiles"

* Build Eclipse projects with C++11 indexing

		-G"Eclipse CDT4 - Unix Makefiles" -D__GXX_EXPERIMENTAL_CXX0X__=1 -D__cplusplus=201103L


[ROS]: http://www.ros.org
