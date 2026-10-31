In 2026, many systems process data near the device instead of sending everything to the cloud. This is called edge computing. In this project, you will set up a Raspberry Pi to work as an edge server for a video camera. The Pi will detect faces on its own and send only a small alert to the cloud instead of sending the full video. This helps reduce the amount of data sent over the network and saves bandwidth.

**Tools and Technologies Used**

- **AWS IoT Greengrass** or **Azure IoT Edge**
- [**Docker**](https://www.upgrad.com/blog/docker-tutorial-learn-from-basics/)
- **OpenCV** (for image processing)

**How to Make It:**

1. Install the IoT Edge software on your Raspberry Pi.
2. Then use Docker to run a container on the Pi that contains your face detection code.
3. Connect a USB camera to the Pi and check that it can process video frames on the device.
4. Set up a cloud dashboard to receive only the number of faces detected, rather than the full video. This helps show how edge computing can reduce network traffic.