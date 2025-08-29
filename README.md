# 项目来源
- 该项目来自于https://github.com/ros-navigation/navigation2的humble分支
- 删除其他包，只保留nav2_controller，nav2_map_server包

# 对于nav2_controller包
- 修改文件navigation2包中nav2_controller/src/control_server.cpp
- 修改原因：publish 0 multi times when 'Goal was canceled. Stopping the robot.' in controller_server
- 修改处：
   ```bashrc
        if (action_server_->is_cancel_requested()) {
        RCLCPP_INFO(get_logger(), "Goal was canceled. Stopping the robot.BySW");
        action_server_->terminate_all();
        // publishZeroVelocity();
        //sw
        rclcpp::Rate rate(5);
        for(int i = 0; i < 10; i++){   #此处增加了重复发0速度的部分
            publishZeroVelocity();
            rate.sleep();
        }
        return;
        }
   ```


# 对于nav2_map_server包
- 修改文件navigation2包中nav2_map_server/src/map_saver/map_saver.cpp
- 修改原因：fix [map_saver]: Failed to spin map subscription bug
- 修改处：
   ```bashrc
        if (map_subscribe_transient_local_) {
        map_qos.transient_local();
        map_qos.reliable();
        map_qos.keep_last(1);
        map_qos.durability_volatile();  #增加了这一行
        }
   ```