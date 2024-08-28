# 原生
- 重置gps服务  
LocationManager towerLocationManager = (LocationManager) getSystemService(Context.LOCATION_SERVICE);
towerLocationManager.sendExtraCommand("gps", "force_xtra_injection", bundle); //快速定位command
towerLocationManager.sendExtraCommand("gps", "force_time_injection", bundle);
towerLocationManager.sendExtraCommand("gps", "delete_aiding_data", bundle); //冷启动
