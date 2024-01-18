<script setup>
import {
  LightbulbFilament24Regular,
  AddCircle32Regular,
  CalendarEdit16Regular,
  Code16Filled,
  ChatBubblesQuestion20Regular,
  ArrowSyncCircle24Regular,
  PlugDisconnected24Regular,
  Code24Filled
} from '@vicons/fluent'
import {
  TimelapseSharp,
  AttachMoneyFilled,
  BrowserUpdatedFilled,
  DiscordFilled,
  PhoneIphoneFilled
} from '@vicons/material'
import {NIcon, NButton, NConfigProvider} from 'naive-ui'
import {UpdateNow} from '@vicons/carbon'
import {Check} from '@vicons/tabler'
import {CodeFilled, CloudUploadOutlined} from '@vicons/antd'
import {TicketOutline} from '@vicons/ionicons5'
import {ref} from 'vue'
import VueWriter from 'vue-writer'
import '../components/Notification.vue'
import axios from 'axios'

const arr = ref(["Ai technology is developing faster and faster, but there are few people who can really use and control it.", "There are many open source projects, but it costs a lot of money to really apply it, such as learning coding, math, computer foundation and so on.", "This is very difficult for many people. For this reason, we wonder why we can't build a universal ai platform.So that people can use and control their own ai without too much effort. ", "This kind of ai is the real ai, embracing technology and life."])
const temName = ref('home')
const show = ref(false)
const email = ref('')
const message = ref('')
const emailRegex = /^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z]{2,}$/;

function getStatus(s) {
  return temName.value === s
}

function changeCompoment(s1) {
  if (temName.value !== s1) {
    temName.value = s1
  }
}

function JudgeEmail() {
  const isEmail = emailRegex.test(email.value);
  if (!isEmail) {
    window.$message.error('Please enter the correct email address!')
    email.value = ''
  }
}

function submitInfo() {
  show.value = true
  if (emailRegex.test(email.value) && message.value !== "") {
    requests()
    setTimeout(
        function () {
          email.value = ''
          message.value = ''
          show.value = false
          window.$message.success('Submitted Successfully!')
        }, 2000
    )
  } else {
    if (!emailRegex.test(email.value)) {
      window.$message.error('Please enter the correct email address!')
      email.value = ''
    } else {
      message.value = ''
      window.$message.error('Please enter the correct message!')
    }
  }
}

async function requests() {
  const options = {
    method: 'POST',
    url: "http://support.ruisibai.store/submit/support",
    headers: {'content-type': 'application/json'},
    data: {
      email: email.value,
      message: message.value
    },
  }
  try {
    const response = await axios.request(options);
    if (response.data.code === 0 && response.data.message === "success") {
    } else {
    }
  } catch (error) {
  }
}

function Judge() {
  console.log(message.value)
}

</script>

<template>
  <n-config-provider :theme="null">
    <div class="homePage">
      <div class="header">
        <span class="nameSpan">RUISIBAI. / 瑞思佰</span>
        <div class="btngroup">
          <n-button @click="changeCompoment('home')" :class="{'btn-1':getStatus('home')}" class="btnn" size="large"
                    quaternary>
            Home
          </n-button>
          <n-button @click="changeCompoment('product')" :class="{'btn-1':getStatus('product')}" class="btnn"
                    size="large"
                    quaternary>
            Product
          </n-button>
          <n-button @click="changeCompoment('priceing')" :class="{'btn-1':getStatus('priceing')}" class="btnn"
                    size="large"
                    quaternary>
            Pricing
          </n-button>
          <n-button @click="changeCompoment('feature')" :class="{'btn-1':getStatus('feature')}" class="btnn"
                    size="large"
                    quaternary>
            Feature
          </n-button>
          <n-button @click="changeCompoment('aboutus')" :class="{'btn-1':getStatus('aboutus')}" class="btnn "
                    size="large" quaternary>
            About Us
          </n-button>
          <n-button @click="changeCompoment('contact')" :class="{'btn-1':getStatus('contact')}" class="btnn "
                    size="large" quaternary>
            Contact
          </n-button>

        </div>
      </div>
      <div v-if='(temName === "home")' class="home">
        <div class="content">
          <div class="texts">
            <h1 class="content_text">RUISIBAI</h1>
            <h1 class="content_text-1">General Purpose AI Platform / 新一代通用人工智能平台</h1>
            <div class="tetx-bac">
              <p class="content_text-2">Discard the cumbersome processes, embrace us, embrace technology.</p>
            </div>
            <VueWriter :iterations='1' :delay="3000" :caret="underscore" class="write" :array="arr" :typeSpeed="47"
                       :eraseSpeed="0"><p><br><br></br>Hello
            </p></VueWriter>
          </div>
        </div>
        <div class="product">
          <div class="card">
            <h4>Best Solution</h4>
            <p>We offers a full-cycle development services.</p>
            <n-icon class="Icon" size="40">
              <LightbulbFilament24Regular/>
            </n-icon>
          </div>
          <div class="card">
            <h4>Saving Time</h4>
            <p>Exchange the least time for the maximum result.</p>
            <n-icon class="Icon" size="40">
              <TimelapseSharp/>
            </n-icon>
          </div>
          <div class="card">
            <h4>General Type</h4>
            <p>Wide coverage and strong applicability.</p>
            <n-icon class="Icon" size="40">
              <AddCircle32Regular/>
            </n-icon>
          </div>
          <div class="card">
            <h4>Low Price</h4>
            <p>High quality, low price is our pursuit.</p>
            <n-icon class="Icon" size="40">
              <AttachMoneyFilled/>
            </n-icon>
          </div>
        </div>

        <div class="services">
          <h1>Product</h1>
          <n-divider style="width: 10%;margin-bottom: 80px;"/>
          <div class="secard">
            <div class="scard">
              <n-icon class="sicon" size="65">
                <UpdateNow/>
              </n-icon>
              <h3>Fast Update</h3>
              <n-divider style="width: 35%;margin-bottom: 30px;"/>
              <p>Relying on the unified deployment of the platform, we can achieve rapid response and rapid update.</p>

            </div>
            <div class="scard">
              <n-icon class="sicon" size="65">
                <BrowserUpdatedFilled/>
              </n-icon>
              <h3>Multi Devices</h3>
              <n-divider style="width: 35%;margin-bottom: 30px;"/>
              <p>The platform makes it possible to achieve a standard experience among multiple devices.</p>

            </div>
            <div class="scard">
              <n-icon class="sicon" size="65">
                <CalendarEdit16Regular/>
              </n-icon>
              <h3>Custom Configuration</h3>
              <n-divider style="width: 35%;margin-bottom: 30px;"/>
              <p>Provide configuration options to the maximum, making it unique.</p>
            </div>
          </div>
          <div class="secard">
            <div class="scard">
              <n-icon class="sicon" size="65">
                <CodeFilled/>
              </n-icon>
              <h3>Online Editing</h3>
              <n-divider style="width: 35%;margin-bottom: 30px;"/>
              <p>You don't need to download any software for online editing.</p>
            </div>
            <div class="scard">
              <n-icon class="sicon" size="65">
                <Code16Filled/>
              </n-icon>
              <h3>Generate Code</h3>
              <n-divider style="width: 35%;margin-bottom: 30px;"/>
              <p>One click to output the specified programming language code.</p>
            </div>
            <div class="scard">
              <n-icon class="sicon" size="65">
                <TicketOutline/>
              </n-icon>
              <h3>Ticket System</h3>
              <n-divider style="width: 35%;margin-bottom: 30px;"/>
              <p>For non-urgent problems, we use the ticket system to solve, and generally give feedback within a
                day.</p>
            </div>
          </div>
          <div class="secard">
            <div class="scard">
              <n-icon class="sicon" size="65">
                <ChatBubblesQuestion20Regular/>
              </n-icon>
              <h3>Live Chat</h3>
              <n-divider style="width: 35%;margin-bottom: 30px;"/>
              <p>For premium members, we have senior customer service specialist at your service 24x7.</p>
            </div>
            <div class="scard">
              <n-icon class="sicon" size="65">
                <DiscordFilled/>
              </n-icon>
              <h3>Discord Integration</h3>
              <n-divider style="width: 35%;margin-bottom: 30px;"/>
              <p>We will first connect to the discord platform, and then we will gradually open channels such as
                Telegram/Slack.</p>
            </div>
            <div class="scard">
              <n-icon class="sicon" size="65">
                <PhoneIphoneFilled/>
              </n-icon>
              <h3>Phone Notification</h3>
              <n-divider style="width: 35%;margin-bottom: 30px;"/>
              <p>Phone notification will be given priority to premium members.</p>
            </div>
          </div>
        </div>
        <div class="services">
          <h1>Programming Language Support</h1>
          <n-divider style="width: 10%;margin-bottom: 80px;"/>
          <div class="progress">
            <n-progress color="black" style="height: 200px;width: 200px;" type="circle" :percentage="80">
              <span style="text-align: center"><h1>80%</h1>Python</span>
            </n-progress>
            <n-progress color="black" style="height: 200px;width: 200px;" type="circle" :percentage="80">
              <span style="text-align: center"><h1>80%</h1>Java</span>
            </n-progress>
            <n-progress color="black" style="height: 200px;width: 200px;" type="circle" :percentage="70">
              <span style="text-align: center"><h1>70%</h1>Golang</span>
            </n-progress>
            <n-progress color="black" style="height: 200px;width: 200px;" type="circle" :percentage="74">
              <span style="text-align: center"><h1>74%</h1>TypeScript</span>
            </n-progress>
            <n-progress color="black" style="height: 200px;width: 200px;" type="circle" :percentage="70">
              <span style="text-align: center"><h1>70%</h1>JavaScript</span>
            </n-progress>
            <n-progress color="black" style="height: 200px;width: 200px;" type="circle" :percentage="45">
              <span style="text-align: center"><h1>45%</h1>C#</span>
            </n-progress>
            <n-progress color="black" style="height: 200px;width: 200px;" type="circle" :percentage="20">
              <span style="text-align: center"><h1>20%</h1>Rust</span>
            </n-progress>
          </div>
        </div>
      </div>
      <div v-if='(temName === "product")' class="realproduct">
        <div class="text">
          <h4>Product Introduction
          </h4>
        </div>
        <div class="boxs">
          <div class="box">
            <div class="question">
              <h4>1.What is RUISIBAI?</h4>
            </div>
            <div class="answer">
              <p>Ruisibai is our vision of a new generation of general-purpose AI functional platform, you can think of it as a complete product, but we choose to use the platform to present it, in our vision, it is a whole, a whole full of ai elements, a thinking whole, a progressive whole.</p>
            </div>
          </div>
          <div class="box">
            <div class="question">
              <h4>2.what is its value?</h4>
            </div>
            <div class="answer">
              <p>Everyone is curious about AI, but most don’t know how to use it or where to apply it.
                The mission of RUISIBAI is to put it in the right place. We will classify and encapsulate all the tedious steps. You only need to click the mouse and enter the name to start your exclusive.</p>
            </div>
          </div>
          <div class="box">
            <div class="question">
              <h4>3.How it is used?</h4>
            </div>
            <div class="answer">
              <p>After building, we will classify and archive all basic AI tools, and assign it a basic startup item. If you do not need too complicated steps, then you can start your experience journey. If you need more complex functions or processes, you need to customize the startup items or add a startup plug-in. After passing the review, it will be applied to the startup of your ai tool.</p>
            </div>
          </div>
          <div class="box">
            <div class="question">
              <h4>4.How does it help me??</h4>
            </div>
            <div class="answer">
              <p>Simply think about a problem, you want to experience or use an AI tool, but don’t know how to start. Learning to code from scratch or aimlessly searching for tutorials on the internet can really waste too much of your time or money. We'll encapsulate the tedious steps so you can just follow the process to get started.</p>
            </div>
          </div>
        </div>
      </div>
      <div v-if='(temName === "feature")' class="feature">
        <div class="text">
          <h4>Feature,Everything You Need.
          </h4>
          <p>All feature only represent the planned and are subject to change at any time, subject to the latest
            data.</p>
        </div>
        <div class="boxs">
          <div class="box">
            <div class="booxicon">
              <n-icon class="boxIcon" size="40">
                <CloudUploadOutlined/>
              </n-icon>
            </div>
            <div class="boxtext">
              <h4>Push To Deploy</h4>
              <p>We plan to support the API upload automatic deployment function, which will break down the barriers
                between the platform and user programs, enabling real-time updates, seamless uploads, and rapid
                deployment.</p>
            </div>
          </div>
          <div class="box">
            <div class="booxicon">
              <n-icon class="boxIcon" size="40">
                <ArrowSyncCircle24Regular/>
              </n-icon>
            </div>
            <div class="boxtext">
              <h4>Data Interoperability</h4>
              <p>In the most common application scenarios, third-party platforms often play an important role. We plan
                to support data calls between different platforms to meet different needs.</p>
            </div>
          </div>
          <div class="box">
            <div class="booxicon">
              <n-icon class="boxIcon" size="40">
                <PlugDisconnected24Regular/>
              </n-icon>
            </div>
            <div class="boxtext">
              <h4>Plugin Loading</h4>
              <p>One program cannot meet all needs. It is planned to support plug-in functions. Premium can customize
                plug-ins within the allowed range and can be added to the startup options after passing the review.</p>
            </div>
          </div>
          <div class="box">
            <div class="booxicon">
              <n-icon class="boxIcon" size="40">
                <Code24Filled/>
              </n-icon>
            </div>
            <div class="boxtext">
              <h4>Programming Language Support</h4>
              <p>We plan to support access to mainstream programming languages on the market and provide calling
                examples. Please note that we will not encapsulate the SDK, only make simple calling cases.</p>
            </div>
          </div>
        </div>
      </div>
      <div v-if='(temName === "aboutus")' class="aboutus">
        <div class="left">
          <h2>About Us</h2>
          <p>We are a young group, full of energy and creativity.
            Change life with technology.</p>
        </div>
        <div class="right">
          <div class="card1">
            <div class="img">
              <img src="../img/younglee.jpg" alt="">
            </div>
            <div class="profile">
              <h3>Young Lee</h3>
              <p>Co-Founder / CEO</p>
              <p>Let technology return to life, let life become leisurely because of technology.</p>
            </div>
          </div>
          <div class="card1">
            <div class="img">
              <img src="../img/wangge.jpg" alt="us avr">
            </div>
            <div class="profile">
              <h3>Ge Wang </h3>
              <p>Co-Founder / Technical Director</p>
              <p>High efficiency, low error, zero loophole, technical helm.</p>
            </div>
          </div>
          <div class="card1">
            <div class="img">
              <img src="../img/jingli.jpg" alt="">
            </div>
            <div class="profile">
              <h3>Jing Li</h3>
              <p>Front-end Engineer</p>
              <p>I will draw the most beautiful page in the world.</p>
            </div>
          </div>
        </div>
      </div>
      <div v-if='(temName === "priceing")' class="productPage">
        <div class="priceText">
          <h4>Pricing plans for teams of all sizes
          </h4>
        </div>
        <div class="sections">
          <p> The following prices apply to different organizations or different uses, please select the option that
            suits you.
          </p>
        </div>
        <div class="priceCards">
          <div class="priceCard">
            <h3>Free</h3>
            <p class="monthly">
              <span>$0</span>
              <span>/month</span>
            </p>
            <div class="items">
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>2 instances</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>1000 Api Requests per month</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>48-hour support response time</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>Generate basic analytics</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>Dashboard setting access</p>
              </div>
            </div>
          </div>
          <div class="priceCard1">
            <h3>Basic</h3>
            <p class="monthly">
              <span>$7</span>
              <span>/month</span>
            </p>
            <div class="items">
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>15 instances</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>100,000 Api Requests per month</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>24-hour support response time</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>Ticket System support</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>Real-time update</p>
              </div>

              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>Multi Devices support</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>Live Chat support</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>Generate code access</p>
              </div>
            </div>
          </div>
          <div class="priceCard2">
            <h3>Premium</h3>
            <p class="monthly">
              <span>$15</span>
              <span>/month</span>
            </p>
            <div class="items">
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>30 instances</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>700,000 Api Requests per month</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>7-hour support response time</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>Code online debugging</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>Phone Notification</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>Platform integration priority experience</p>
              </div>
              <div class="item">
                <n-icon class="Icon" size="27">
                  <Check/>
                </n-icon>
                <p>New function testing</p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <di v-if='(temName === "contact")' class="contact">
        <n-spin stroke="#1F2225" :show="show">
          <form class="form">
            <div class="title">Contact us</div>
            <input @change="JudgeEmail" v-model="email" type="text" placeholder="Your email" class="input">
            <textarea v-model="message" @change="Judge" placeholder="Your message"></textarea>
            <button type="button" @click="submitInfo">Submit</button>
          </form>
        </n-spin>
      </di>

      <div class="footer">
        <h3>© 2024 RUISIBAI, Inc.</h3>
      </div>

    </div>
  </n-config-provider>

</template>
<style scoped>

.realproduct .boxs {
  height: 70%;
  width: 100%;
  //background-color: black;
  display: flex;
  .box{
    flex-direction: column;
    .question{
      h4{
        font-size: 30px;
        font-weight: 400;
      }
    }
    .answer{
      p{
        font-size: 20px;
        color: #4B5563;
        text-indent: 40px;
      }
    }
    border: 1px solid gray;
    border-radius: 10px;
    padding: 15px;
  }
  .box:hover{
         transform: scale(1.03);
        border: 2px dashed gray;
       }
}

.realproduct .text {
  h4 {
    font-size: 40px;
  }

}

.boxtext {
  height: 100%;
  width: 78%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;

  h4 {
    font-size: 20px;
    font-weight: 500;
  }

  p {
    color: #4B5563;
    font-size: 14.5px;
  }
}

.boxIcon {
  padding: 7px;
  background-color: #C2C2C2;
  color: white;
  border-radius: 20%;
}

.booxicon {
  height: 100%;
  width: 22%;
}

.box {
  background-color: white;
  height: 45%;
  width: 45%;
  margin: 10px;
  display: flex;

}

.boxs {
  height: 70%;
  width: 80%;
  padding: 50px;
  box-sizing: border-box;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.feature .text {
  h4 {
    font-size: 40px;
  }

  p {
    color: #4B5563;
    font-size: 20px;
  }

  display: flex;
  flex-direction: column;
  //justify-content: space-between;
  align-items: center;
}

.feature {
  margin-top: 80px;
  height: calc(100vh - 207px);
  width: 100%;
  background-color: #FFFFFF;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.realproduct {
  margin-top: 80px;
  height: calc(100vh - 207px);
  width: 100%;
  background-color: #FFFFFF;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.item p {
  margin-left: 10px;
}

.item {
  display: flex;
  justify-content: start;
  width: 100%;
}

.items {
  margin-top: 0px;
  display: flex;
  width: 100%;
  flex-direction: column;
  justify-content: space-evenly;
  height: 80%;
}

.monthly span:last-child {
  color: #4B5563;
  font-weight: 600;
}

.monthly span:first-child {
  font-size: 35px;
  font-weight: 700;
}

.monthly {
  margin-top: 10px;
}

.priceCard h3 {
  font-size: 20px;
}

.priceCard2 {
  height: 90%;
  width: 20%;
  //background-color: black;
  border-radius: 20px;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
  border: 1px solid #E5E7EB;
  border-left: 0;
  box-sizing: border-box;
  padding: 20px;
}

.priceCard1 {
  height: 100%;
  width: 20%;
  //background-color: black;
  border-radius: 20px;
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
  border: 1px solid #E5E7EB;
  padding: 20px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
}

.priceCard {
  height: 90%;
  width: 20%;
  //background-color: black;
  border-radius: 20px;
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
  border: 1px solid #E5E7EB;
  border-right: 0;
  display: flex;
  flex-direction: column;
  padding: 20px;
  box-sizing: border-box;
}

.priceCards {
  display: flex;
  margin-top: 30px;
  height: 65%;
  width: 100%;
  justify-content: center;
  align-items: end;
}

.sections {
  width: 30%;
  text-align: center;
  margin-top: 10px;
  color: #4B5563;

}

.priceText {
  //height: 100px;
  color: black;
  font-size: 40px;
}

.productPage {
  margin-top: 80px;
  height: calc(100vh - 207px);
  width: 100%;
  background-color: #FFFFFF;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.card1 .profile {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  width: 50%;

  h3 {
    font-size: 30px;
    font-weight: 400;
  }

  h3 ~ p {
    font-size: 20px;
    color: #4B5563;
  }

  p:last-child {
    font-size: 15px;
    color: #4B5563;

  }
}

.card1 img {
  height: 100%;
  //width: 100%;
  border-radius: 10px;
  margin-right: 100px;
}

.card1 {
  display: flex;
  height: 30%;
  justify-content: start;
}

.aboutus .right {
  width: 50%;
  margin-left: 7%;
  display: flex;
  flex-direction: column;
  height: 85.5%;
  padding: 50px;
  justify-content: space-evenly;

}

.aboutus .left h2 {
  font-size: 40px;
}

.aboutus .left p {
  color: #4B5563;
  font-size: 20px;
}

.aboutus .left {
  height: 100%;
  width: 23%;
  display: flex;
  flex-direction: column;
  align-items: start;
  justify-content: center;
  margin-left: 230px;
}

.aboutus {
  margin-top: 100px;
  height: calc(100vh - 227px);
  width: 100%;
  display: flex;

}

.contact {
  margin-top: 140px;
  height: calc(100vh - 267px);
}

.is-typed {
  font-family: "JetBrains Mono";
}

.is-typed span.cursor {
  display: inline-block;
  width: 3px;
  background-color: black;
  animation: blink 1s infinite;
}

.write {
  font-size: 25px;
  color: #FF4081;
}

.home {
  width: 97%;
}

.footer h3 {
  color: white;
}

.footer {
  margin-top: 50px;
  width: 100%;
  height: 77px;
  background-color: black;
  display: flex;
  justify-content: center;
  align-items: center;
}

.progress {
  width: 85%;
  display: flex;
  justify-content: space-evenly;
}

.btnn {
  margin-right: 30px;
}

.scard h3 {
  font-weight: 500;
  font-size: 25px;
}

.sicon {
  margin-bottom: 15px;
  padding: 15px;
  background-color: #c2c2c2;
  border-radius: 50px;
}

.scard:hover {
  border: 3px dashed #FF4081;
  border-radius: 10px;
  transform: scale(1.07);
}

.scard {
  height: 250px;
  width: 400px;
  border: 3px solid black;
  position: relative;
  padding: 30px;
  transition: all 0.2s linear;
}

.secard {
  height: 40vh;
  width: 80%;
  display: flex;
  justify-content: space-evenly;
}

.services {
  width: 100%;
  margin-top: 100px;
  margin-bottom: 50px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.card .Icon {
  position: absolute;
  top: 20px;
  right: 20px;
}

.card:hover {
  top: -20px;
  transition: all 0.5s ease 0s;
  background-color: #1E2022;

  h4, p, .Icon {
    color: white;
  }

}

.card p {
  font-size: 16px;
  color: #777181;
  margin-top: 20px;
}

.card h4 {
  font-size: 25px
}

.card {
  position: relative;
  top: 0;
  height: 150px;
  width: 350px;
  margin: 0 20px;
  padding: 25px;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  transition: all 0.15s linear;
  border: 1px solid #FFFFFF;
  border-radius: 10px;
  box-shadow: 0 0 10px gray;
}

.product {
  min-width: 330px;
  width: 100%;
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 50px 0;


}

.btn-1 {
  background-color: rgba(46, 51, 56, .09);
}

.tetx-bac {
  display: flex;
  align-items: center;
  justify-content: center;
}

.content_text-2 {
  backdrop-filter: blur(1px);
  font-size: 20px;
}

.content_text-1 {

  font-size: 45px;
}

.texts {
  text-align: center;
  color: black;
  font-size: 50px;
  margin: auto;
}

.btngroup {
  margin-right: 30px;
}

.content {
  min-width: 650px;
  width: 100%;
  height: 90vh;
  background: repeating-radial-gradient(circle, #fff, #fff 5px, #000 6px);
  background-size: 50px 100px;
  display: flex;

}

.nameSpan {
  font-weight: 400;
  font-size: 30px;
  margin-left: 30px;
  margin-right: auto;
}

.header {
  min-width: 820px;
  height: 80px;
  background-color: #FFFFFF;
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  width: 100%;
  top: 0;
  border-bottom: 1px solid #EFEFF5;
  box-shadow: 0 0 100px gray;
  z-index: 40
}

.homePage {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;

  .form {
    height: 468px;
    position: relative;
    display: flex;
    align-items: flex-start;
    flex-direction: column;
    gap: 10px;
    width: 600px;
    background-color: white;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 30px 30px -30px rgba(27, 26, 26, 0.315);
  }

  .form .title {
    font-size: 30px;
    font-weight: 600;
    letter-spacing: -1px;
    line-height: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .form input {
    outline: 0;
    border: 1px solid rgb(219, 213, 213);
    padding: 8px 14px;
    border-radius: 8px;
    width: 100%;
    height: 50px;
  }

  .form textarea {
    border-radius: 8px;
    height: 300px;
    width: 100%;
    resize: none;
    outline: 0;
    padding: 8px 14px;
    border: 1px solid rgb(219, 213, 213);
  }

  .form button {
    align-self: flex-end;
    padding: 8px;
    outline: 0;
    border: 0;
    border-radius: 8px;
    font-size: 16px;
    font-weight: 500;
    background-color: black;
    color: #fff;
    cursor: pointer;
  }

  .form button:hover {
    background-color: #4b4848;

  }

}
</style>