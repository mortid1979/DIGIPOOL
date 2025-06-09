
# 🏊‍♂️ Digipool Modbus Dashboard for Home Assistant

Monitor and control your Digipool heat pump or water system directly from Home Assistant using Modbus. This package includes:
- 🔌 Modbus configuration for Digipool registers
- ⚙️ Automations for temperature control
- 📊 A Lovelace dashboard for real-time monitoring

---

## 📁 Included Files

| Path                             | Purpose                             |
|----------------------------------|-------------------------------------|
| `config/modbus.yaml`            | Modbus sensor definitions           |
| `config/automations.yaml`       | Automations (e.g. adjust temp)      |
| `dashboards/digipool_lovelace.yaml` | Dashboard card configuration        |

---

## 🚀 Setup Instructions

### 1. 🔧 Configure Modbus Access
Make sure your Digipool device supports Modbus over TCP.

In `config/modbus.yaml`, **replace** this line:

```yaml
host: ENTER_YOUR_DIGIPOOL_IP_HERE
```

With your actual Digipool device IP address (e.g. `192.168.1.45`).

---

### 2. 🧩 Include Files in Home Assistant

In your `configuration.yaml`, add:

```yaml
modbus: !include config/modbus.yaml
automation: !include config/automations.yaml
```

Also make sure you have:

```yaml
input_number:
  digipool_water_temp_setpoint:
    name: Set Water Temperature
    min: 20.0
    max: 32.0
    step: 0.5
    unit_of_measurement: "°C"
```

---

### 3. 💻 Import the Dashboard

In the UI:
- Go to **Dashboards > Raw Configuration Editor**
- Paste contents of `dashboards/digipool_lovelace.yaml` into a new view or card
- Save and refresh

---

## 📡 Available Sensors

These sensors are defined and used:

- `sensor.preferred_water_temp`
- `sensor.water_temp_outlet`
- `sensor.current_power`
- `sensor.sum_kwh_meter`
- `sensor.daily_pump_energy`
- `input_number.digipool_water_temp_setpoint`

---

## ⚡ Electricity Pricing Integration (Optional)

Automations are configured to respond to dynamic electricity pricing. You can use:

- Your own pricing sensor (e.g. `sensor.nordpool_kwh_be_eur_3_10_006`)
- Or replicate the logic using your own **ENTSO-e**, **Nordpool**, or **external** API

Update the automation trigger in `config/automations.yaml` with your sensor name and threshold.

---

## 🙋‍♂️ FAQ

**Q: My sensors show `unavailable`.**
A: Check:
- That your Digipool IP is correct
- Modbus is enabled on the device
- Port 502 is reachable

---

## 📢 Credits

Created by the Home Assistant community with ❤️  by Dieter Mortier
For support or suggestions, open an issue or pull request on GitHub.
