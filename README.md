# 项目来源
- 该项目来自于https://github.com/ros-navigation/navigation2
- 删除其他包，只保留nav2_controller，nav2_map_server包

# 对于nav2_controller包
- 修改文件navigation2包中nav2_controller/src/control_server.cpp
- 修改原因：publish 0 multi times when 'Goal was canceled. Stopping the robot.' in controller_server   

# 对于nav2_map_server包
- 修改文件navigation2包中nav2_map_server/src/map_saver/map_saver.cpp
- 修改原因：fix [map_saver]: Failed to spin map subscription bug