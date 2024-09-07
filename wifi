// 定义参数解析函数
function argsList(argsString) {
  const args = {};
  argsString.split('&').forEach(arg => {
    const parts = arg.split('=');
    args[parts[0]] = parts[1];
  });
  return args;
}

// 获取传入的参数
const args = argsList(typeof $argument === "string" && $argument || '');

// 解析 WiFiList 参数，如果没有传入，则默认为空数组
const WIFI_DONT_NEED_PROXYS = args.WiFiList ? args.WiFiList.split(',') : [];
const CURRENT_WIFI_SSID_KEY = 'current_wifi_ssid';

if (wifiChanged()) {
  const mode = WIFI_DONT_NEED_PROXYS.includes($network.wifi.ssid)
    ? 'direct'
    : 'rule';
  $surge.setOutboundMode(mode);
  $notification.post(
    'Surge',
    `Wi-Fi changed to ${$network.wifi.ssid || 'cellular'}`,
    `use ${mode} mode`
  );
}

function wifiChanged() {
  const currentWifiSSid = $persistentStore.read(CURRENT_WIFI_SSID_KEY);
  const changed = currentWifiSSid !== $network.wifi.ssid;
  if (changed) {
    $persistentStore.write($network.wifi.ssid, CURRENT_WIFI_SSID_KEY);
  }
  return changed;
}

$done();
