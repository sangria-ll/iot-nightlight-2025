[Back to README](../README.md) | [Previous: Step 5](step5.md) | [Next: Step 6 - Bonus Upgrades!](step6.md)

# Step 5: Control Your Nightlight from the Web

Now you can turn your nightlight ON, OFF, or set it to NIGHTLIGHT mode (automatic) from your web browser!

## What You'll Do
- Update your code to add web-based mode control (On, Off, Nightlight)
- Use the web page to control your nightlight's mode
- Instantly see the light sensor value and nightlight status

## Instructions

### 1. Update Your Code

1. Open your [`main.py`](../my_nightlight/main.py).
2. **Add a `mode` variable at the top of your script:**
   ```python
   mode = 'nightlight'  # Modes: 'nightlight', 'on', 'off'
   ```
3. **Replace your current `web_page` function with this new one:**
   ```python
   def web_page():
       led_state = "ON" if led.value() else "OFF"
       sensor_value = sensor.read()
       html = f"""
       <html><head><title>Nightlight Status</title></head><body>
       <h1>ESP32 Nightlight</h1>
       <p>Light Sensor Value: <b>{sensor_value}</b></p>
       <p>Nightlight is: <b>{led_state}</b></p>
       <p>Current Mode: <b>{mode}</b></p>
       <form action="/" method="get">
           <label for="mode">Set mode:</label>
           <select id="mode" name="mode">
               <option value="nightlight" {'selected' if mode == 'nightlight' else ''}>Nightlight (auto)</option>
               <option value="on" {'selected' if mode == 'on' else ''}>On</option>
               <option value="off" {'selected' if mode == 'off' else ''}>Off</option>
           </select>
           <input type="submit" value="Set Mode">
       </form>
       </body></html>
       """
       return html
   ```
4. **In your main loop, update the LED logic to use the selected mode:**
   ```python
   while True:
       value = sensor.read()
       if mode == 'on':
           led.on()
       elif mode == 'off':
           led.off()
       else:  # nightlight mode
           if value < threshold:
               led.on()
           else:
               led.off()
       # ...existing code for handling web requests...
   ```
5. **Update your web request handling to parse the mode from the URL:**
   ```python
   # Inside your main loop, after receiving a request:
   if 'GET /?mode=' in request_str:
       try:
           mode_str = request_str.split('GET /?mode=')[1].split(' ')[0]
           new_mode = mode_str.split('&')[0]
           if new_mode in ['on', 'off', 'nightlight']:
               mode = new_mode
               print('Mode updated to', mode)
       except Exception as e:
           print('Error parsing mode:', e)
   ```

### 2. Use the Web Interface

1. Save and upload your updated [`main.py`](../my_nightlight/main.py) to the ESP32.
2. Open your web browser and enter the ESP32's IP address (shown in the serial console).
3. On the web page, you'll see:
   - The current light sensor value
   - Whether the nightlight is ON or OFF
   - The current mode (Nightlight, On, Off)
   - A dropdown menu to set the mode
4. **To change the mode:**
   - Select "Nightlight (auto)" to let the sensor control the light
   - Select "On" to turn the light on
   - Select "Off" to turn the light off
   - Click "Set Mode" to apply your choice
5. The page will refresh and show the new mode and status instantly.

**Tip:** Use "Nightlight" mode for automatic control, or "On"/"Off" for manual control.

---

🎉 You can now control your nightlight from anywhere on your WiFi!

[Next: Step 6 - Bonus Upgrades!](step6.md)
