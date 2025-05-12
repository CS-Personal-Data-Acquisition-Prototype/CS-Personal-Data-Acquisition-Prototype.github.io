
## **Software Requirements Specification for Personal Data Acquisition Prototype**

# **1\. Overview**

## **1.1 Problem Description**

Personal data acquisition systems are systems that gather sport performance data on the way the athlete and the equipment they are using or operating is performing and provides feedback where improvements can be made. Today’s personal data acquisition systems largely fall into two categories. Category one is professional data acquisition systems, which provide the user high quality data to analyze. However, these systems are expensive, difficult to install, create a massive amount of data to transmit and store, and possibly require a high acumen with computer systems if something goes wrong. Category two is more cost-efficient Do It Yourself (DIY) systems. These systems solve the cost issue of professional systems and depending on the number and type of sensors, can reduce the amount of data that is transmitted and processed. The trade-off for the DIY systems is that the level of programming and computer systems expertise required grows exponentially.

In between these two categories, there is a void that leaves many people looking to improve their performance by accessing the power of data acquired while performing their sport.

## **1.2 Purpose and Vision**

Our project will fill the void between the professional and DIY data acquisition systems that are available today. We will build a low cost modular data acquisition system that will be simple to install and use. We aim to create an easy-to-use, real time user interface that allows any user to install the system and use the data effortlessly, improving their performance without a significant background in computer systems. Our data acquisition system will have the capability to locally store and live stream the most important data for instant feedback.

## **1.3 Users and Stakeholders**

- Alex Ulbrich  
- Kirsten Winters  
- Chris Patton (Project Partner)  
- OSU Global Formula Racing club  
- Feipeng Yue (Winter 2025 TA)  
- ECE 44X Team  
- Group Members  
  - Bradley Tyler  
  - Colby Noah  
  - Garrett McMichael  
  - Joey Abruzzo  
  - Lisa Young  
  - Max Goldstein  
  - Morgan Padberg

Chris Patton is carrying out the role of project partner. He has stated that he will be able to provide us with previous years’ GitHub repositories, testing data for our prototype, and some amount of contact with the Global Formula Racing club at OSU. He has provided us with a basic framework for how our prototype should function, as well as constraints in the form of a preferred programming language (Rust). Chris Patton and the teaching team for this project (Alex Ulbrich, Kirsten Winters, and Casey) all have a stake in this project due to the time that they are investing in it. For the project partner, this investment may extend to a financial one.

We are using the OSU Global Formula Racing club as a proxy for our assumed user base. This means that when we perform user experience surveys, they will be our respondents. It is also possible that they will be able to make actual and significant use of our prototype if we are able to meet their needs.

We are working on this project alongside an ECE team. Since our product requires hardware that we will have to purchase, both teams have a financial stake in the outcome of this project. As a stretch goal we are also considering the possibility of turning the final prototype into a purchasable product, which will result in an even greater time and work investment. Moreover, our grades in the class depend partly on the successful implementation of the product.

# **2\. Preliminary Context**

## **2.1 Assumptions**

The product we are developing is a prototype personal data logger for amateur F1 cars. The data logger will receive information from six sensors: accelerometer, yaw rate, GPS, force transducer, linear potentiometer, and string potentiometer. It will record data at 100Hz \- 5,000Hz and live stream the information to a website on a remote device.

We will be using Rust for the majority of the coding, as requested by the project partner, along with choosing either egui or OpenGL, though wgpu, for the graphics.

## **2.2 Constraints**

We may be limited by the fact that we are primarily using Rust since none of the team members have coded in Rust before. Moreover, previous teams for this project have stated that using Rust and egui for the frontend resulted in a primitive UI, and suggested that Rust and egui be avoided for frontend. This results in a tradeoff: if we use egui, we will have the expertise of our project partner but most likely have a lacking end result. On the other hand, if we use Rust and OpenGL, we may no longer be using a coding language and library that the project partner is familiar with, but could end up with a much more sophisticated UI. However, if that UI is limited in functionality, the project may fall short of these requirements.

Our prototype will be transmitting a large amount of data. This means that we will need to perform a significant amount of data compression to properly display the data in a timely and readable manner.

## **2.3 Dependencies**

We need a database to hold the data from the data logger, user logins and user settings.

We are building off previous years work and will need to adapt to the current data logger being set up by the ECE team.

We are building a web application and will need to design a prototype and get feedback from the Oregon State University GFR Team prior to coding the User Interface.

Getting realistic test data and access points to the data logger require us to be dependent on other stakeholders.

## **2.4 Market Assessment and Competition**

- Oregon State University’s Global Formula Racing team currently uses [Vector](https://www.vector.com/us/en/) for data collection  
  - High cost ([https://www.ebay.com/itm/324655452701](https://www.ebay.com/itm/324655452701))   
- [Dragy](https://dragymotorsports.com/) GPS data logger popular with vehicle tuners  
  - Corresponding mobile app has a rating of 1.1 stars on the App Store, with users reporting that the performance report and other features do not load properly  
  - High cost  
    - GPS and performance recorder is $229.00  
    - Company promotes accessories that cost up to $39.50  
- JB Data Engineering  
  - $3350 entry point  
  - High technical knowledge required to install

## **2.5 Target Demographics**

The ideal target demographic for this project would be hobbyist or low-level professionals who are less technically proficient or more time constrained. Existing products have a high capability ceiling that can be used by professionals or high-level hobbyists with enough time to dedicate to them, but have a high barrier to entry. Our project will have a lower capability ceiling, but lower barrier to entry since it should take significantly less time to get up and running and produce useful results. Examples include hobbyist and small club-level racers or mountain bikers. These users might be limited by budget or software knowledge, or might have limited time to spend on their sport. They need quick access to important data, but might not need all the advanced features offered by competing products.

# **3\. System Requirements Specification**

## **3.1 Functional Requirements**

- The user should be able to view real-time or historic data from any selection or subselection of sensors connected to the device.  
- The client should receive information in real-time from the device when a stable connection is available.  
- When a stable connection is available between the device and server or the device and client, the client should receive real-time data.  
- If the device loses connection with the database/web server, the user should be able to view all data captured during the disconnection period when the device reconnects.  
- After a connection interruption, the client should automatically resume real-time data streaming from the device.  
- The client should be able to manually or automatically synchronize databases with the device.  
- The user interface should be easy for new users to navigate.  
- The web interface should be able to handle both mobile and desktop screen sizes.  
- The user interface should provide multiple color-blindness accessibility modes.

## **3.2 Non-Functional Requirements**

- The UI should have user selectable light and dark themes.  
- The software should have encrypted user passwords and usernames both when at rest or being transmitted.  
- Device should record data at 100Hz \- 5000Hz.  
- The live streaming data should refresh at least every 2-3 seconds.  
- The device should upload its local data to the remote server frequently to minimize latency.  
- The device should immediately delete data from local memory once successfully uploaded to conserve RAM and minimize wear to the device’s flash memory.

## **3.3 Data Requirements**

- Data should be collected from a variety of sensors and may include:  
  - Accelerometer  
  - Yaw Rate  
  - GPS  
  - Force transducer  
  - Linear potentiometer  
  - String potentiometer  
- Data should be stored locally, then transmitted wirelessly and stored in database  
- Data must be filtered in order to provide accurate information

![][image1]  
**Figure 1–Database Entity-Relationship Diagram**

## **3.4 Integration Requirements**

- Rust will be used for the embedded software to capture the data and prepare it to be sent to the external database  
  - Data formatting  
  - Error handling  
  - Local data storage  
- A remote database will store the data collected by the tracker and also be used to retrieve the data as it is displayed on the user interface

## **3.5 User Interaction and Design**

- The UI should be visually appealing and simple to navigate  
- To reduce clutter sub-menus and pages can be used, but should be limited to reduce complexity  
- Accessibility options like light and dark mode and colorblind modes should be available  
- Graphs should be easily readable and make good use of colors  
- Icon use should be clear and easy to understand  
- Icons should be prioritized over text wherever possible  
- Pages on the website should load in under 2 seconds and provide smooth visual transitions  
- Interface should always be clear about what is happening, and the user should never be stuck on a blank page or infinite loading icon

## **3.6 Open Questions**

What are the sensors the ECE team is creating measuring? Which sensor is measuring what data?

What is the speed at which the hardware will develop data for each sensor used?

## **3.7 Out of Scope**

We will not be implementing a mobile specific application.

We are considering a subscription service as a form of revenue, but this is currently a stretch goal. Doing so would also require more maintenance past the scope of the class.

# **4\. Project Timelines** 

## **4.1 Milestones**

| Due Date                                | Feature                           | Description                                                                                                                                                                                                          | Dependencies                                              |
| --------------------------------------- | --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| CS 461 Week 7                           | Tech Stack Design                 | Determine the technology stack to use and what resources are required to develop this project, so we can note this in our design document and have all resources available by the start of CS 462\.                  |                                                           |
| CS 461 Week 7                           | Version-Control Setup             | Configure a version-control system repository to host project code on GitHub                                                                                                                                         |                                                           |
| CS 461 Week 7                           | Low-Fidelity Design               | Create a flow or wireframe UI design to understand the broad layout of the application                                                                                                                               |                                                           |
| CS 461 Week 8                           | High-Fidelity Design              | Create a high-fidelity UI design for the frontend of the main web application for the design document, project partner, and demo assignment.                                                                         | Low-Fidelity Design                                       |
| CS 461 Week 8                           | Tech Stack Resources              | Ensure all resources determined necessary in *Tech Stack Design* are requested/ordered.                                                                                                                              | Tech Stack Design                                         |
| CS 461 Week 9                           | Local Development                 | Create a test database and webapp to ensure proper communication between the webapp and the DBMS.                                                                                                                    | Tech Stack Design                                         |
| CS 461 Week 10                          | Development Server Configuration  | Once the requested development server is available to the team, install software required in *Tech Stack Design*; grant access to team members as needed. Ensure that the webapp is accessible from the Internet.    | Tech Stack Resources Local Development (partial)          |
| CS 462 Week 1                           | Database Schema Implementation    | Design and implement the schema for how the sensor data will be stored, both on the local device and on the remote server.                                                                                           |                                                           |
| CS 462 Week 2                           | Mock Data Generation              | Write code to generate data that would emulate a sensor; this is used to test Week 4 code.                                                                                                                           | Database Schema Implementation                            |
| CS 462 Week 4                           | Network Protocol Implementation   | Design the protocol used to transmit sensor data from the local device and the remote server; implement code to connect the local database with the TCP client and to connect the TCP server to the remote database. | Mock Data Generation                                      |
| CS 462 Week 6                           | Remote Recorded Sensor Data Table | Write code to make the web UI display a table of recorded (mock) sensor data.                                                                                                                                        | Network Protocol Implementation                           |
| CS 462 Week 6                           | Sensor Implementation             | Design the protocol for communicating between the Bluetooth-enabled sensors and the local device.                                                                                                                    | Database Schema Implementation *ECE team’s sensor design* |
| CS 462 Week 7                           | Remote Sensor Graph               | Write code to add a graph of sensor data to the recorded data table page in the UI, and controls to configure the graph display.                                                                                     | Remote Recorded Sensor Data Table                         |
| CS 462 Week 7                           | Remote Live Sensor Readout        | Write the code to make the web UI display a live readout of sensor data. Optionally, include a bar graph in addition to the numeric readout.                                                                         | Network Protocol Implementation                           |
| CS 462 Week 9                           | Remote Live Sensor Graph          | Add a dynamically updating graph to the live sensor readout page to show recently collected data of a selection of sensors.                                                                                          | Remote Sensor Graph                                       |
| CS 462 Week 10 (and periodically after) | Configuration Page                | Add a page on the web UI to manage the configuration of both the server and the device. As additional features are added, update this page with necessary controls to configure these features.                      |                                                           |
| CS 463 Week 2                           | Data Management                   | Add a mechanism to the UI to export data to a standardized format (CSV, XLS(X), JSON, etc.); add mechanisms to select and delete data.                                                                               | Remote Recorded Sensor Data Table                         |
| CS 463 Week 4                           | Out-of-Box Experience             | Create an “initial setup” screen where a user can intuitively configure the device, sensors, and server at first run                                                                                                 | Sensor Implementation Configuration Page                  |
| CS 463 Week 5(ongoing until then)      | Documentation                     | Proofread documentation created throughout the project; create a table of contents or other method of searching documentation.                                                                                       | Completion of software                                    |
| CS 463 Week 6 (due 2025-05-13 12:00)    | Engineering Expo Poster           | Create a poster showcasing the project’s features and design to present at the Engineering Expo.                                                                                                                     |                                                           |
| CS 463 Week 6                           | User Testing                      | Complete final user experience surveys to gather any achievable goals within remaining time.                                                                                                                         | Completion of software                                    |
| If time permits                         | Stretch Goals                     |                                                                                                                                                                                                                      |                                                           |

**Table 1–Weekly Project Milestones**

## 

## **4.2 Goals and Success Metrics**

| Goal                                                                                           | Metric                                                                | Baseline | Target | Tracking Method                                                            |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- | -------- | ------ | -------------------------------------------------------------------------- |
| Increase usability of product among people with low technical expertise                        | Percentage of survey participants that found the software easy to use | 75%      | 90%    | Usability study with OSU F1 team                                           |
| Desired features, or equivalent alternatives, are present (compared to previous iterations)    | Percentage of features included                                       | 75%      | 90%    | Compare prototype features with desired features found in previous studies |
| Desired features, or equivalent alternatives, are present (compared to currently used product) | Percentage of features included                                       | 70%      | 80%    | Compare prototype features with current OSU F1 software (Vector)           |

**Table 2–Identifiable Project Goals and Tracking Metrics**

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnAAAACxCAYAAABEOICbAAAjCElEQVR4Xu2dMY4byc/F9yhOF1jAV3A03huMb+B8AYcLGD6AU8NwamzsC/yj9QEcGo4n9KRO58PT4unjUFWtUXeTana9H9CQuqqLZBUpFtWakX57EEIIIYQQpfjNNwghhBBCiG2jAk4IIYQQohgq4IQQQgghiqECTgghhBCiGCrghBBCCCGKoQJOCCGEEKIYKuCEEEIIIYqhAk4IIYQQohgq4IQQQgghiqECTgghhBCiGCrghBBCCCGKoQJOCCGEEKIYKuCEEEIIIYqhAk4IIYQQohgq4IQQQgghiqECTgghhBCiGCrghBBCCCGKoQJOCCGEEKIYKuCEEEIIIYqhAk4IIYQQohgq4IQQQgghiqECTgghhBCiGOEF3G+/hasQG0G+FlFkxlamLjEWiq1xyPB1uIaMSYhtIF+LKDJjK1OXGAvF1jhk+DpcQ8YkxDaQr0UUmbGVqUuMhWJrHDJ8Ha4hYxJiG8jXIorM2MrUJcZCsTUOGb4O15AxCbEN5GsRRWZsZeoSY6HYGocMX4dryJiE2AbytYgiM7YydYmxUGyNQ4avwzWsPYmvX78eZC6V+/z584fPnz/75ouBDNgCed+/f/fdofz8+fO4Fjim5vPr16/D9ZEs9Ukl1vI74hnHUl6/fn2MA/h6b2TGVqauCBgLeFwSC+/evQvPGaNRPbZaIE5evnx5jBXFzX9k+Dpcw5qTQFAgUJCUkJyuHSTYuLGBYwOGXbApE8wfLxbAwrZHxotqSv+euLbfWzCBwqapQr4qmbGVqSsCxsK5N3Uin+qx1UIFXJsMX4drWHMS3DhtsKANSYpFHR6hExsZ77LZPo5lnw0+PAJbDE0Fo70byHe6bPPFJuykrbwOh22zdkDvuaLMFnAAciAP46CX6wU4D7Tzjs/Su0eeKVv3xFP8Drjm8AvW2sYh+xgHwPsfMJZtWwvaYzdsu5FDBnTT5zYucB1tZBvG2fiijGuRGVuZuiJgLBD6mDHKWMDh+3xsIAZsG3MMYtjGkgrFp1E9tlrYPZTnNre19jjGoY2jvZHh63ANa0+CH11RLhMKsMFh9bKos3dKmHTsxmgLoJb8FhhLfRjHYGbf/f398W6h3RBtMgW2j5uptaOFHQOsrdYunvMFxqS79gtnyta9cc7vLNJsYmMBZz/aYpJr+Z9+wiPH9YAe2uNjjQUaxtsiEXAetNH2Aeq387gGmbGVqSsCxoL1NV//NhZwjX8DYot0jrHFPePKvhm2OVRMUz22Wvg8x7jxMdXKSfZN7d7I8HW4hqhJwPkIjKkCyyYxgEe0MSGtUcARyIBMu5EDG6A2gAlt+PHjx8kGfmkBh+d3d3eP9NmNmi8qvqBUwC2n53dC/9u1sRvpuQKO8XuugCO8FnHgY40ybFzYPhZyts/bcS0yYytTVyTwGYt2HwsEfXa+iD3GAXNGr4BjnpmSLx6zl9iycA9jfmDc+H67xxEVcMsI17DmJJhc+BwbCw48t4Hg71rYzQzjsWGygOPGazeupxZw3LzRTzkcS3m9Ao5yfSLkOFx3SQHHuzXAJl6OZxvXC89VwM3jUr/TNz7G7AG8/23bVAHHfh9jHMuY9wUcbcTRip+WrGuRGVuZutbGxgLjyMcoHn2OYZFm49bmDMZGL28xTsQ0lWOrh40hm+N6sWJzku3bGxm+Dtew9iSQKCDTyuU5NxheYwsUPEcbEw0LOHs9+55awDH4vC4WTgzM1uYKaDfHTdnRgi8EHpwP5NGmm5ubg26bvO0YFg9rMGXrnniK34H1D9voG66VLeC8/8FTCjjA+MbBZEgbGReUYZMsn1sbgbURqICrA2OBecfGq80RPifavMlz+tzmFOA3ZRVwT6N6bPVg7uvlEeZIH4cq4JYRriFjEtHYZNcK0mhsAuZhC4etsAdfbx0bAzhG2TgzYytTlxgLxdY4ZPg6XEPGJMQ2kK9FFJmxlalLjIViaxwyfB2uIWMSYhvI1yKKzNjK1CXGQrE1Dhm+DteQMQmxDeRrEUVmbGXqEmOh2BqHDF+Ha8iYhNgG8rWIIjO2MnWJsVBsjUOGr8M1ZExCbAP5WkSRGVuZusRYKLbGIcPX4RoyJiG2gXwtosiMrUxdYiwUW+OQ4etwDc+ePTtMRMf+D/g6E69fx36PzNhSzhrryESxNc6RkbPCoxcT2ToVbKxA9XWsbv+eyfRNhK4ImaIeioNxyPB1uIaMSSylgo0VqL6O1e3fM5m+idAVIVPUQ3EwDhm+DteQMYmlVLCxAtXXsbr9eybTNxG6ImSKeigOxiHD1+EaMiaxlAo2VqD6Ola3f89k+iZCV4RMUQ/FwThk+DpcQ8YkllLBxgpUX8fq9u+ZTN9E6IqQKeqhOBiHDF+Ha8iYxFIq2FiB6utY3f49k+mbCF0RMkU9FAfjkOHrcA1LJvH9+/fDeB5fv349tD9//vzh8+fPh+doe/36tR12MedshI6pa2BnD4yFredk7IFrzw9+QGzYmGG7jZeenb32tZjSvUVgL46fP38+WlOuZSaZ69bS5WPr0lzUkrkm9NVTYSzCty9fvryqb0eiFQetfY7xRtDeiy2xTVq+XptwDUsm0dp48cikiUckn6X0bIQO9L179+54jX2x/fr16/Ci4osL5+xDYrQbn7Ufjx8/fnwk279YKb8SvXVcipU7pYNJz8YMkyHa8Ih4gV9a9GQzDuxYttHvdoPnRurH2QLOxgZgLL1582bSxpYeyvV6eB2hPspuycI5bIAt//vf/w7tuB5xSvB8jdfdJfR8s5SW3FZba0O9JBe1ZAIbI76NG7bNOYTnHMdYByzI+DqAHOYpHyMs4Mg1fLt3vN88rX2O8cbHXj7o4WXa1zdjl32tuEAc/P3338ecxFgB3LM4Bo/MGXj+5cuXR/FndYxEy9drE65hySR8EDLwEITv378/BvhSejZCPoKVActNFqANum0CpL28Do9M8NZ+vkAolzJwPV9sftOsQG8dl2LlTumYKuAQL1jjqXjpyaZMjIdPrC/Zxk2SG6BNvH6cjRnayFjxc/D09DDmcFAPwHXQx9i0cWX1WN2M8V4ssmDJpOebpbTkttq4NuTSXDQl08eDzwnMJS1f+jiyvqKNGO9jy+sh1/Dt3jmXv+hPQL/QV/DNHH94mcwxjCXIhe8ZDz53IIZ4PWRZeXZvYx6iPIxlfrIxZ3WPQsvXaxOuYckk4HyMx2ETJJ4zeJbIJz0Z1OmTHYMZjzYB0h5rr0+Y9pHJksF9f39/eKQMm1gr0FvHc7x48eI450sOD9eb/Ux8bGc8Ye1btGQC61cmO2sH/ES/4mAB5MfxGrtJet8zudqCyeL1WB04IJfXAMYpsLYAJl0+Z9L1ib9yAWfX5pLD42Pr0lzU67P+YyxYO7D21ufcAL2t9JX1NzdlHsxV0OlzGrmGbysyN2fRX5bWPmdzFv11CdyjAGMDUA9zjbXL5g482qLLvzFg4WYfAfMH48jnJ8bmCLR8vTbhGpZMwgahhUHCIOcmNJeejQxkG9S8lvptArTJk9BWL4PJFv2td9kV6a3jOc6Ns/1T1zIefMzYOEJ/rzCekg3Qz6Rkix8L2q0c+tsnR15zaQFHqKe14bbi1PZxY+AjuKSA4/wzOeebubTkttq4Xp6n5qKWTEJ/cbNurS3zjI1tO46+4gHmFHA9/eIxU/702Gtb41r7nI03PO/lmx5Wpo0JADk2d/j8wBzVKuBs21MKuFZ+GoWWr9cmXMOSSbQCG9hNBoG1NEB6NjKY+S4C8Pnt7e3xRWE3dPQxMQK+o8bfE/GFwcdWAQcog+dV6K3jOc6Ns/1T1z6lgPMblqUnG2PpE/qcbfQbdaONycyPo++BjRXQSowtWnoolzFo9bC4AH4OVhav6RVwHIvDr28GnM/atOS22uyGanlqLmrJBDZGfBviAUC3v8b6A9hNmsU9z59SwF3TtxXp+bOF95untc/5eIOPerHVgz6lv8FTcwceWwWclXFzc3PonyrgvI6RaPl6bcI1ZExiKRVsrMDcdTw37u3bt83na3PODnE9onzTiqcIXREyxfW4xJ82xi4ZJ2qT4etwDRmTWEoFGyswdx3njlubrdghTsn0TYSuCJniesz159xxoh4Zvg7XkDGJpVSwsQJz13HuuLXZih3ilEzfROiKkCmux1x/zh0n6pHh63ANGZNYSgUbKzB3HeeOW5ut2CFOyfRNhK4ImeJ6zPXn3HGiHhm+DteQMYmlVLCxAnPXce64tdmKHeKUTN9E6IqQKa7HXH/OHSfqkeHrcA0Zk1hKBRsrMHcd545bm63YIU7J9E2ErgiZ4nrM9efccaIeGb4O15AxiaVUsLECc9dx7ri12Yod4pRM30ToipAprsdcf84dJ+qR4etwDRmTWEoFGyswdx3njlubrdghTsn0TYSuCJniesz159xxoh4Zvg7XkDGJpVSwsQJz13HuuLXZih3ilEzfROiKkCmux1x/zh0n6pHh63ANGZNYSgUbKzB3HeeOW5ut2CFOyfRNhK4ImeJ6zPXn3HGiHhm+DteQMYmlVLCxAnPXce64tdmKHeKUTN9E6IqQKa7HXH/OHSfqkeHrcA0Zk1hKBRsrMHcd545bm63YIU7J9E2ErgiZ4nrM9efccaIeGb4O15AxiaVUsLECc9dx7ri12Yod4pRM30ToipAprsdcf84dJ+qR4etwDRmTWEoFGyswdx3njlubrdghTsn0TYSuCJniesz159xxoh4Zvg7X0JvE9+/fH54/f37ox/H169dDO9o+f/58eI62169fP/z69evROI7BgWtfvnz58O7du2M/zn/+/Hlo43U479GzcS0wD86vArQXa+bXeoq56zh3XAvrcxyIBx6AcddiTTs8WE8bx1O8evXqsPZ+/SvF0NpE+sbT02VjCzGEWLq5uXkUW8xDnp5MUZO5/pw7rip+/ybMcZdybg/aEhm+DtfQm4TdSOFgFl0s4LBZYax3MsZ5J7KAo0wmVG56kN9LrKBn46jYAo7rRn9Mgf6//vrLN5/lnNxLgL3e17aAQ3z0CqE17ViCLeBo61ThOQLwzd3d3aO2t2/fPjpfi14c+LgCLODO+acnU1wf5CwfW+eY68+546qiAi6WcA29SfiEx2ILbe/fv39UiFl6BdybN2+OMjwYg0Dq0bORxSQLRFtUog2BCbk40I82zovXgF5BxOKSc7V3Hy1TetiHR8ijfBbEXC+rm3pwWN1co5a9ANe3fEK4jkiIdsP99OnTwx9//HF4/u+//x6fk976z6FXwGE+9EePnh1cX8QYZEEO44x91Ilzu248p6/RTl9x46fPKatVwAFcOyfp7QHGE2KLG27PX0vpyfVxBVDAwUet162lJRP+hK8B4wNyoAd+RjzgGuiwr3O+Tv1rn/HE1yj7mBdxzrzARxagzC2jwniyb0CRp5Cv+Bx5jLT8+RTmjrsU+JT+REwxRpg/GGOMFe4R9hzPmfNub28fXcdcavMZ93PmWxufHrvX8Rr7yRkOtHMv8vva1BvxrZDh63ANvUnAyXS4dR7aMAZHK6FgHPttMmIbkxth/1SC7dlIWwjssYF7f39/0IdrGKScl9XHIOQBGNyQYefRmjOvtXpYfPE5N3vqZWHG9bL2sI86vc20ky8m8tQCDtiE+Pvvvx8TIbDPQW/95wB7GQuUa2Nmil6/T0L0F2Cx5f3mz7GejBcAeVxPrin1qIA7xfqGbxB6/lpKT66NLfqFOWIqv4CWTPizV8ARnDNmWjHE53bzJa2NkXYyxngNZPvcORr2DQLW0ucs5DHS8udTmDvuUmxeacWGL+BA6xxxgtj48uXL4ZwFHeOWenAN90bGMvC5k9g/PfDX8DXAAs7C10arb2tk+DpcQ28ScB4LEAsLCfb7DQvtPlmy8LEFCWDCZWD16NlI0A9bbAHnYRFJEFw4Z3DbA9gCziZav/F7qMcWcMTKZ5Fm+9g2t4DjGvew87+kgFsT2OjXkEkG2OLLcy4OmDR8wrEgsdl15znG+c2XcU57zhVwuL6nd+9Y31yzgPNwI4KferkBtGRiHDdC71tunr6gs0Vbq4Dj6xYwnvjYKuBacxqVSwq4ubTiIAKb8/jcxpj3uz+3ewHz/sePHw/PbdxSNvMix5wr4OxHqD5OfczbnEu7VMD9R7iG3iTgdF+AAFtI4JFBRwcyEC228GHAARZedkNt0bMR7ZQHHXiONhY+fEQ/+/gIGPhoY2K1djLQzxVwLT1cPzueMgHnbdtoM9eYRSBlTRVwPX9ZOO9LP0JdE9jr19AmM/Qx0Xh6cUB5rY9QuaY2sbTO6WvIoq9ol09krQLuKeu/ZxhPW/wI1cZWa7MCLZmt1zBkIHbge7ThGugA6PNvAvgc1/P1judWppcNGGO0f+p1MQKXfoQ6l1YcRACf2n0U/ucj87rNPejz55SDvIdx+BiV8cU3Kzaf2Vj0e5tnqoDjXmff/PK1Z/Mqc+NWyfB1uIbeJHobki0k4GCcf/v27ehcG5jEFj64xhZSPC59dwygh+MZLGxjsHIeaLNBxnHAF1G2rxW4LVp6OEfOzeqxhaufA2XxGp63Cji7hn7dPbjGbrAWJD/0413sGomwB9bGryHnCGzy8dAnHvjHzt/6gnLpV+9nnjOhMT6pyyZNxoEt4Oz6bz1hRcI1sBtsz19L6cn1cQVsAceiq0VPJmIKsYS7G9xcW7GDc7QzXwD7HONgB+MLMv3HpK0CzspmHI6Gf8NJkKeQr9C3Vs7qxcHaIBaYt5jvmE9wzpjg64pFFs9tjPmYoXwrG3FkY59yWPx5WgUc4x4f17JA87GpAu4x4RrWmAScyyQZQc9GBqGO/z/+/PNPv0xH0F+Z6vbvmUzfROiKkCnqkRUH9o3hNeGbDLuHtG7c7JEMX4dryJjEUirYWIHq61jd/j2T6ZsIXREyRT0UB+OQ4etwDRmTWEoFGytQfR2r279nMn0ToStCpqiH4mAcMnwdriFjEkupYGMFqq9jdfv3TKZvInRFyBT1UByMQ4avwzVkTGIpFWysQPV1rG7/nsn0TYSuCJmiHoqDccjwdbiGjEkspYKNFai+jtXt3zOZvonQFSFT1ENxMA4Zvg7XkDGJpVSwsQLV17G6/Xsm0zcRuiJkinooDsYhw9fhGjAJHeMclXnx4oVvEhshM7YQBz6udez3yCRbn7geGb4O15AxiaVUsLEC1dexuv17Rr4Re0BxPA4Zvg7XkDGJpVSwsQLV17G6/XtGvhF7QHE8Dhm+DteQMYmlVLCxAtXXsbr9e0a+EXtAcTwOGb4O15AxiaVUsLEC1dexuv17Rr4Re0BxPA4Zvg7XkDGJpVSwsQLV17G6/XtGvhF7QHE8Dhm+DteQMYmlVLCxAtXXsbr9e0a+EXtAcTwOGb4O15AxiaWcs/Hr168PL1++9M0H3r179/D582ff3OT79+8PP3/+fNQG2b9+/XrUBlrXbp1z65gB/AE7eGAdeQA8Pn/+3I36j2vZDz+/evXq8NzbL/5DayH2wJ7iGDmLebXH1N5JkP961/T2xwpk+DpcQ8YkltKzkZs9NlUGGIo1XI92Pud429cC8t6/f//oGgYoDivLXnvuRbIVeuuYCXyFw8ICDokC692jZz+LKsplXKCNRTaSGQ60ox960I+44TWvX78+tNGGm5ubw/Hjx49HBZwF/VX8HwlfG3/99Zfvevj9998PfXgUYsv0ckwEzFHcu5B3kGfsnsLcxn3o9vb2cP7hw4dj4fTmzZuH+/v7h48fPx73Pe5XOMdzn9tae6eH43DwGozzNnN/xHWVyPB1uIaMSSylZyOCCMHKILTvJrjR8g5cq8+D4GQfXwQMULTznAUHr0XgVngX0lvHTHoF3FPeCfbs5/ojkUEWY8H2MXnhHPr57hR+5h1aXssiD48Y4+/AWTBmqugcBazv3d3doYDDgefg06dPD//+++/hOR5xLsRW6eWYtbFvVu3eYvcb9gHkH7ymeI7xLPK4V/HNKN9UMsfZnMvc5vfOFuhjfsO62Dtx1ma0V8yDGb4O15AxiaX0bGTAMljtOw2OQaAxwH2fB3J4N4ZyEZR44dgghzx77VNuVW+B3rwz6RVwXNOpJNCzn3dWWYjRxziYsFicMWmxQGO7T6i4Dn5F+1QBZ4vFkbFrzuPZs2cnPvPXCLElsmKSRREP5j7eCECe8Z9IsGAizGNot302f7FYs7rQ5/dOD4s12mQLOW8z7vzhzTNtr0KGr8M1ZExiKT0bucEyCBGYvI3LzZzB3OrzQA4LMT5HgOL2NMeyCLDXVvkYrbeOmfQKOK4fE0uLc/YzybAo8322gCM8twkQ1z61gKvi+2isb3AHjgnef2zqz4XYEudyzFrYYq3V5nMS8OfIU/gzHvZxX7P5i3ujz1F+7/TYos0+5z5I2M99thIZvg7XkDGJpfRsRPDhLgqCGIHFdw04vnz5cgxqjG/1eSCPf9fGO24MUBx85+Gv7RUcW6O3jpmcK+DopxY9++F79DGBMC5YRPAaW8AxLmyxRzlMkr0CjnHQs2dEuB76GzhRmczXNHOU/3trwBxpc5Iv4GxBxSLK5i/0+b+B8zmSe2cLjsOBO2wA43o2q4A7JVxDxiSWUsHGClRfx+r27xn4hn/3JkRVKuUYe9fLF3fiPBm+DteQMYmlVLCxAtXXsbr9eybTN5m6xFgotsYhw9fhGjImsZQKNlag+jpWt3/PZPomU5cYC8XWOGT4OlxDxiSWUsHGClRfx+r275lM32TqEmOh2BqHDF+Ha8iYxFIq2FiB6utY3f49k+mbTF1iLBRb45Dh63ANGZNYSgUbK1B9Havbv2cyfZOpS4yFYmscMnwdriFjEkupYGMFqq9jdfv3TKZvMnWJsVBsjUOGr8M1ZExiKRVsrED1daxu/57J9E2mLjEWiq1xyPB1vAYhhChERuLNgF8ijfnoO7y2wV5iS5wnw9fxGoQQohAZiTcaFG78nV7CXyGxBR2e47cm8Wi/RR/ndh18G+Tj10NaP6Mk+uwhtsTTyPB1vAYhhChERuLNgD+lxDtxOGeRhuco4li44bA/i2R/Ao59AEUgf0fTXiOexl5iS5wnw9fxGoQQohAZiTcD/xuVvIPGg20o5GyRxsIOB38Dk78frAJuGXuJLXGeDF/HaxBCiEJkJN5o8LEmf7Ccd97snTV+vOoLOH7MCtCOgz9MDnAdzlXAzWMPsSWeRoav4zUIIUQhMhJvBryLxkKu9zdw/g6c/3s328ZrVMDNYy+xJc6T4et4DUIIUYiMxCvGRLE1Dhm+jtcghBCFyEi8Ykz2FFtP+Q9k3N3lR/I97Mf2How/d5eXd5i3Roav4zUIIUQhMhKvGJPM2OJ/Idu/aUTRhTYWXih++DE6CqXb29vD+YcPH46F05s3bx7u7+8PXzfDv6dEHz9St/8sw4/m+XeT9h9gPByHg9fwo3prM67jtS2gAwf/w5qP1ybD1/EahBCiEBmJV4xJVmzhrhaLKf7XMP8pBc9514qPKOzu7u4e/b0kizwWbCiq0H5zc3Po4x04FlCA/xyDazFuqoBDH4oy/tezvRNnbUY7r2uBa9HHv8nsFXrZZPg6XoMQQhQiI/GKMcmKLRZFPFBU2Y8jUfTYIg+wYCK4hv9xbPt4t4sFHP8xhgf6WOyx0POwWKNNtpDzNuPOH+4C0nYPiz3IYNG4BTJ8Ha9BCCEKkZF4xZhkxZYt1lpt9g4X8ecoiN6/f3/s40eTLJRYwLX+Fg5tUwWcLdrsc3/3jP0sGluwYGPxZudwTTJ8Ha9BCCEKkZF4xZhkxZa9u4bChue2gLOP+Fj027dvJ3fgWl8bc+4jVBZi5z5CRX/vI1Rvc68QBNTNu4EYtwUyfB2vQQghCvHs2bNHH+Xo2PeRSba+Jdi7Xv7unDhPhq/jNQghRCEiEm+ETFGPKnFg77jxfEkB54vmuX+ntpacDDJ8Ha9BCCEKEZF4I2SKeigOxiHD1/EahBCiEBGJN0KmqIfiYBwyfB2vQQghChGReCNkinooDsYhw9fxGoQQohARiTdCpqiH4mAcMnwdr0EIIQoRkXgjZIp6KA7GIcPX8RqEEKIQrcSL75jib0vi4H/k8bchQeuLSElLZib2vwoxF87DzkXEc+04EHlk+DpegxBCbJRWkm21sYAjLHxYwOGx94WloCUTYCz67Fi22d92xE8JoY1fUoqvT2ABZr+c1Y7jF6Ti+Pvvvx8VcPb7vXpFp1ifXhyI/ZHh63gNQgixUVpJttU2VcDh54b4I949pmTab6D330rPAgvX2sKL+m0bv4Uej/xJIer1d+DszxJt+bu09kYrDsQ+yfB1vAYhhLgSvAN16eHxH6GyWEMbDt796tHr83fSUGRZO+7u7o6FF4ozFlv2Ol/I8Y6gCrjt0YsDsT8yfB2vQQghNkorybba/B04wo9Q7d20Fi2ZhIUWZPjfjrSFly3gCHTj+h8/fhz7Ling9BFqLlNxIPZFhq/jNQghxEZpJdlW27kCDuDR3tmytGTaAgvFF3+8G23+I1RfwPEjW9s/5yNUe42IR2s9Dhm+jtcghBAb5e3bt74pJPFGyBT1UByMQ4av4zUIIUQhIhJvSybatnKIHLTW45Dh63gNQghRiIjEGyFT1GNPcfDq1avjP/P0wEf0U1+vsyawpfc3qNcgw9fxGoQQohARiTdCpqhHZhzwv6btV9Sg6EIbCy/+FzT68PeRt7e3h/MPHz4czgG+g/D+/v7h48ePx7/5RB+uwzn/vpJyAP9m1P9TjoV/f8m/3WzJQbu95ubm5nDgOXTYPjzy+RbI8HW8BiGEKERE4o2QKeqRFQcogFjI8M6UbUNhhYKJhRLAuf0nHBZ1/GcZ9mEsnvMOHIomykEBxkKRRRaee9Dn7+BRDgu51lgUb2i3d/Y4P92BE0KIwYlIvBEyRT2y4oB3t3iw6OFdNftfz8QXdLiGxZvtaxVwVhe/2maqgAO8S2f/i9rKsUUaYWHYmp8KOCGEGJyIxBshU9QjKw5scYaCiue2gLOPuLP17du3kwKOX53Du2J45F0wFnC4zn69DWTgWujtfYTK8bCLX79DOSzs+LEoQD9kcozv0x04IYQQIYk3QqaoR2Yc8G/gWIS1Cjj7N2f+DhwLMYA++/dyHOv/Bo4fs7IIw8/M9b4oGtdiDAvDnhyc844eCzjbx/mxqNtKEZfh63gNQghRiIjEGyFT1KNKHNg7bjy3xd2lYN72YAG5ZzJ8Ha9BCCEKEZF4I2SKeigOxiHD1/EahBCiEBGJN0KmqIfiYBwyfB2vQQghChGReCNkinooDsYhw9fxGoQQohARiTdCpqiH4mAcMnwdr0EIIQoRkXgjZIp6KA7GIcPX8RqEEKIQEYk3Qqaoh+JgHDJ8Ha9BCCEKEZF4WzL5vVZCCDGH06wihBAD0yq2ltKSyS8t/eeff45fdoovJ8WPh+McPx6O/taXmgohxGlWEUKIgWkVW0tpybR34Pjj4ijeUKjxp4jYZ38Xcms/GSSEuA6nWUUIIQamVWwtpSXTFnAo0Hj3jd+Cb388vPXj3UKIsTnNKkIIMTCtYmspLZn+b+Dwm44szFDA4cA5fjy89ePdQoixOc0qQggxMK1iayktmbzTZos2/vYknvsfD/c/3i2EGJvTrCKEEAPTKraWMiXT/3A4sB+hCiFEi35WEUKIAZkqtuYSIVMIMTbKKkIIYYgotiJkCiHGRllFCCEMEcVWhEwhxNgoqwghhCGi2IqQKYQYG2UVIYQwRBRbETKFEGOjrCKEEIaIYitCphBibJRVhBDC8OLFi0PBpWOMQ4iqKHqFEEIIIYqhAk4IIYQQohgq4IQQQgghiqECTgghhBCiGCrghBBCCCGKoQJOCCGEEKIYKuCEEEIIIYqhAk4IIYQQohgq4IQQQgghiqECTgghhBCiGCrghBBCCCGKoQJOCCGEEKIYKuCEEEIIIYqhAk4IIYQQohgq4IQQQgghiqECTgghhBCiGCrghBBCCCGK8X+t2C+RD/R1KgAAAABJRU5ErkJggg==>