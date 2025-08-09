[Back to README](../README.md) | [Previous: Step 3](step3.md)

# Step 4: Monitor Your Nightlight from a Web Browser

In this step, you'll make your ESP32 serve a web page that shows the current light level and whether the nightlight is on or off.

## What You'll Do
- Connect your ESP32 to WiFi
- Create a simple web server in MicroPython
- View the nightlight status and sensor value from a web page

## Instructions

1. **Open your [`main.py`](../my_nightlight/main.py) file.**
2. Add your WiFi credentials at the top of your script:

```python
WIFI_SSID = "e3CivicHigh"
WIFI_PASSWORD = "e3Griffins!"
```

3. **Connect your ESP32 to WiFi.** Add this code after your WiFi credentials:

```python
import network
import socket

station = network.WLAN(network.STA_IF)
station.active(True)
station.connect(WIFI_SSID, WIFI_PASSWORD)

# Wait for connection
while not station.isconnected():
    pass

print('Connected, IP address:', station.ifconfig()[0])
```

4. **Define a function to generate the web page.** Place this code after your sensor and LED setup:

```python
def web_page():
    led_state = "ON" if led.value() else "OFF"
    sensor_value = sensor.read()
    html = f"""
    <html><head><title>Nightlight Status</title></head><body>
    <h1>ESP32 Nightlight</h1>
    <p>Light Sensor Value: <b>{sensor_value}</b></p>
    <p>Nightlight is: <b>{led_state}</b></p>
    </body></html>
    """
    return html
```


5. **Set up the web server socket.** Add this code after the `web_page` function:

```python
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(('', 80))
s.listen(1)
s.setblocking(False)  # Make the socket non-blocking so your loop keeps running
print('Web server started!')
```

6. **Combine your sensor/LED logic and web server in the same loop.** Replace your main loop with this code:

```python
while True:
    # 1. Update the LED based on the sensor value
    value = sensor.read()
    if value < threshold:
        led.on()
    else:
        led.off()
    # 2. Check for a web request (non-blocking)
    try:
        conn, addr = s.accept()
        print('Got a connection from %s' % str(addr))
        request = conn.recv(1024)
        response = web_page()
        conn.send('HTTP/1.1 200 OK\n')
        conn.send('Content-Type: text/html\n')
        conn.send('Connection: close\n\n')
        conn.sendall(response)
        conn.close()
    except OSError:
        pass
    time.sleep(0.1)  # Small delay to avoid hogging the CPU
```

5. **Upload and run your script.**
   - Open the serial console to see your ESP32's IP address.
   - Enter the IP address in your web browser to view the nightlight status and sensor value.
   - You can adjust the `threshold` variable in your code to change when the nightlight turns on.

---

[Next: Step 5](step5.md)