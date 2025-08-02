+++
title = "Timeline of my experience"
template = "timeline.html"
+++
<!-- experience timeline -->
<div class="timeline">

  <div class="timeline-item">
    <div class="timeline-content">
      <div class="timeline-description">
        <div class="container">
          <div class="image">
            <img src="/images/VT.png" height="100" width="100">
            <br>
            <br>
            <div class="timeline-date">2023-2025</div>
            <hr>
          </div>
          <div class="text">
                    <img src="/images/world_example.png" height="140" width=auto style="float:right; margin-right: 15px;">
            Master of Science in Computer Engineering at Virginia Tech through the Accelerated Master's Program.<br><br>
            My thesis focused on robotics and I worked under the advisory of Professors Thinh Doan and Michael Hsiao.
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="timeline-item">
    <div class="timeline-content">
      <div class="timeline-description">
        <div class="container">
          <div class="image">
            <img src="/images/JSEG.png" height="74" width=auto>
            <br>
            <div class="timeline-date">2024</div>
            <hr>
          </div>
          <div class="text">
                    <video controls="" height="200" width=auto name="Load Simulating Actuator" style="float:right; margin-left: 15px;" autoplay="" muted="">
                        <source src="/videos/actuator.MOV">
                    </video>
                        I worked with the Jacobs Space Exploration Group as a Thrust Vector Control Intern, developing the active hardware and software components of their new Active Inertial Load Simulator at NASA's Marshall Space Flight Center.<br><br>
                        In this video you can see an actuator modeling the dynamics of a mass-spring-damper.
                    <!-- <img src="/images/VAB.jpg" height="200" width=auto style="float:right; margin-left: 15px;"> -->
                        <!-- Hardware elements that I aided in the integration of included measurement equipment such as an LVDT and full-bridge pancake load cell and test equipment such as an industrial electromechanical actuator (EMA), which entailed characterization testing and modeling of the physical characteristics of the actuator.<br><br> -->
                        <!-- The software that I developed included a non-linear model of the EMA and software tools used to test EMAs. -->
                        <!-- In this video you can see the characterized EMA in the closed-loop system being used to model the dynamics of a mass-spring-damper! -->
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="timeline-item">
    <div class="timeline-content">
      <div class="timeline-description">
        <div class="container">
          <div class="image">
            <img src="/images/VT.png" height="100" width="100">
            <br>
            <br>
            <div class="timeline-date">2020-2024</div>
            <hr>
          </div>
          <div class="text">
                    Bachelor of Science at Virginia Tech with a double major in Computer Engineering and Electrical 
                    Engineering (with focuses in Machine Learning and Controls, Robotics & Autonomy, respectively).<br><br>
                    <!-- During my undergraduate studies I also worked on two design teams: Solar Car and Human Powered Submarine. -->
                    <!-- For Solar Car I worked with Leads to develop the overall E/E architecture of the car and  -->
                    <!-- designs for the car's lithium-ion battery. -->
                    <!-- For the Human Powered Submarine I used a single board computer to develop a GUI for the submarine pilot, -->
                    <!-- aiding them in navigating and guiding the submarine.<br><br> -->
                    <!-- <img src="/images/pacman.png" height="110" width=auto style="float:left; margin-right: 15px;"> -->
                    <!-- I also participated in undegraduate research with Professors Thinh Doan and Michael Hsiao, developing  -->
                    <!-- symbolic reinforcement learning architectures to play atari games. -->
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="timeline-item">
    <div class="timeline-content">
      <div class="timeline-description">
        <div class="container">
          <div class="image">
            <img src="/images/G2ELAB.png" height="74" width=auto>
            <br>
            <div class="timeline-date">2023</div>
            <hr>
          </div>
          <div class="text">
                    <img src="/images/INV.png" height="130" width=auto style="float:right; margin-left: 15px;">
            I was a Research Intern at the Grenoble Electrical Engineering Laboratory (G2ELab) in Grenoble, France, working on inverter control systems for microgrids &ndash; small power grid systems aiming to avoid future infastructure problems on the French power grid.<br><br>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="timeline-item">
    <div class="timeline-content">
      <div class="timeline-description">
        <div class="container">
          <div class="image">
            <img src="/images/NAVSEA.png" height="74" width=auto>
            <br>
            <div class="timeline-date">2022</div>
            <hr>
          </div>
          <div class="text">
            I was a Concept Research Intern at the Center for Innovation in Ship Design (CISD), working on the Hospital "Sea-Train" concept.<br><br>
          </div>
        </div>
      </div>
    </div>
  </div>

</div>

<!-- css for timeline -->

<head>
    <style>
        .timeline {
            position: relative;
            margin: 30px;
            padding: 40px 20px;
        }
        .timeline::after {
            content: '';
            position: absolute;
            width: 3px;
            background-color: #007A59;
            top: 0;
            bottom: 0;
            margin-left: -1px;
        }
        .timeline-item {
            position: relative;
            margin-bottom: 50px;
        }
        .timeline-item::after {
            content: '';
            position: absolute;
            width: 21px;
            height: 21px;
            background-color: #007A59;
            border-radius: 50%;
            top: 0;
            margin-left: -10px;
        }
        .timeline-item.left .timeline-content {
            left: 70%;
        }
        .timeline-item.right .timeline-content {
            left: 20%;
        }
        .timeline-content {
            position: relative;
            left: 30px;
        }
        .timeline-date {
            font-weight: bold;
            margin-bottom: 10px;
            text-align: right;
        }
        .timeline-description {
            font-size: 20px;
            margin-bottom: 10px;
        }    
        .image img {
          max-width: 100%;
          border-radius: 5px;
          border: 0px;
          float: left;
        }
    </style>
</head>

