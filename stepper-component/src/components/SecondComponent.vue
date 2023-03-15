<script>
export default {
    name: "Secondomponent",
    data() {
        return {
            newQuestions: [],
            score: 0,
            countdown: 3,
            currentQuestion: 0,
            timer: 20,
            hidbutton: true,
            hidediv: false,
            countTimerInterval: null,
            checkedAnswear: [],
            questions: [
                {
                    text: 'Why is AWS more economical than traditional data centers for applications with varying compute workloads?',
                    choices: [
                        { id: 'a', text: 'Amazon EC2 costs are billed on a monthly basis', selectedChoice: null },
                        { id: 'b', text: 'Users retain full administrative access to their Amazon EC2 instances', selectedChoice: null },
                        { id: 'c', text: 'Amazon EC2 instances can be launched on demand when needed', selectedChoice: null },
                        { id: 'd', text: 'Users can permanently run enough instances to handle peak workloads', selectedChoice: null },
                    ],
                    correctAnswear: 'c',
                    explanation: 'The ability to launch instances on demand when needed allows users to launch and terminate instances in response to a varying workload. This is a more economical practice than purchasing enough on-premises serversto handle the peak load'
                },
                {
                    text: 'Which AWS service would simplify the migration of a database to AWS?',
                    choices: [
                        { id: 'a', text: 'AWS Storage Gateway' },
                        { id: 'b', text: 'AWS Database Migration Service (AWS DMS)', selectedChoice: null },
                        { id: 'c', text: 'Amazon EC2', selectedChoice: null },
                        { id: 'd', text: 'Amazon AppStream 2.0', selectedChoice: null },
                    ],
                    correctAnswear: 'b',
                    explanation: 'AWS DMS helps users migrate databases to AWS quickly and securely. The source database remains fully operational during the migration, minimizing downtime to applications that rely on the database. AWS DMS can migrate data to and from most widely used commercial and open-source databases'

                },
                {
                    text: 'Which AWS offering enables users to find, buy, and immediately start using software solutions in their AWS environment?',
                    choices: [
                        { id: 'a', text: 'AWS Config', selectedChoice: null },
                        { id: 'b', text: 'AWS OpsWorks', selectedChoice: null },
                        { id: 'c', text: 'AWS SDK', selectedChoice: null },
                        { id: 'd', text: 'AWS Marketplace', selectedChoice: null },
                    ],
                    correctAnswear: 'd',
                    explanation: 'AWS Marketplace is a digital catalog with thousands of software listings from independent software vendors that makes it easy to find, test, buy, and deploy software that runs on AWS.'
                },
                {
                    text: 'Which AWS networking service enables a company to create a virtual network within AWS?',
                    choices: [
                        { id: 'a', text: 'AWS Config', selectedChoice: null },
                        { id: 'b', text: 'Amazon Route 53', selectedChoice: null },
                        { id: 'c', text: 'AWS Direct Connect', selectedChoice: null },
                        { id: 'd', text: 'Amazon Virtual Private Cloud (Amazon VPC)', selectedChoice: null },
                    ],
                    correctAnswear: 'd',
                    explanation: 'Amazon VPC lets users provision a logically isolated section of the AWS Cloud where users can launch AWS resources in a virtual network that they define.'
                },
                {
                    text: 'Which of the following is an AWS responsibility under the AWS shared responsibility model?',
                    choices: [
                        { id: 'a', text: 'Configuring third-party applications', selectedChoice: null },
                        { id: 'b', text: 'Maintaining physical hardware', selectedChoice: null },
                        { id: 'c', text: 'Securing application access and data', selectedChoice: null },
                        { id: 'd', text: 'Managing guest operating systems', selectedChoice: null },
                    ],
                    correctAnswear: 'b',
                    explanation: 'Maintaining physical hardware is an AWS responsibility under the AWS shared responsibility model'
                },
                {
                    text: 'Which component of the AWS global infrastructure does Amazon CloudFront use to ensure low-latency delivery?',
                    choices: [
                        { id: 'a', text: 'AWS Regions', selectedChoice: null },
                        { id: 'b', text: 'Edge locations', selectedChoice: null },
                        { id: 'c', text: 'Availability Zones', selectedChoice: null },
                        { id: 'd', text: 'Virtual Private Cloud (VPC)', selectedChoice: null },
                    ],
                    correctAnswear: 'b',
                    explanation: 'To deliver content to users with lower latency, Amazon CloudFront uses a global network of points of presence (edge locations and regional edge caches) worldwide.'
                },
                {
                    text: 'How would a system administrator add an additional layer of login security to a users AWSManagement Console?',
                    choices: [
                        { id: 'a', text: 'Use Amazon Cloud Directory', selectedChoice: null },
                        { id: 'b', text: 'Audit AWS Identity and Access Management (IAM) roles', selectedChoice: null },
                        { id: 'c', text: 'Enable multi-factor authentication', selectedChoice: null },
                        { id: 'd', text: 'Enable AWS CloudTrail', selectedChoice: null },
                    ],
                    correctAnswear: 'a',
                    explanation: 'Multi-factor authentication (MFA) is a simple best practice that adds an extra layer of protection on top of a  username and password. With MFA enabled, when a user signs in to an AWS Management Console, they will be  prompted for their username and password (the first factor—what they know), as well as for an authentication  code from their MFA device (the second factor—what they have). Taken together, these multiple factors provide increased security for AWS account settings and resources.'
                },
                {
                    text: 'Which service can identify the user that made the API call when an Amazon EC2 instance is terminated?',
                    choices: [
                        { id: 'a', text: 'AWS Trusted Advisor', selectedChoice: null },
                        { id: 'b', text: 'AWS CloudTrail', selectedChoice: null },
                        { id: 'c', text: 'AWS X-Ray', selectedChoice: null },
                        { id: 'd', text: 'AWS Identity and Access Management (AWS IAM)', selectedChoice: null },
                    ],
                    correctAnswear: 'b',
                    explanation: 'AWS CloudTrail helps users enable governance, compliance, and operational and risk auditing of their  AWS accounts. Actions taken by a user, role, or an AWS service are recorded as events in CloudTrail. Events  include actions taken in the AWS Management Console, AWS Command Line Interface (CLI), and AWS SDKs and APIs'

                },
                {
                    text: 'Which service would be used to send alerts based on Amazon CloudWatch alarms?',
                    choices: [
                        { id: 'a', text: 'Amazon Simple Notification Service (Amazon SNS)', selectedChoice: null },
                        { id: 'b', text: 'AWS CloudTrail', selectedChoice: null },
                        { id: 'c', text: 'AWS Trusted Advisor', selectedChoice: null },
                        { id: 'd', text: 'Amazon Route 53', selectedChoice: null },
                    ],
                    correctAnswear: 'a',
                    explanation: 'Amazon SNS and Amazon CloudWatch are integrated so users can collect, view, and analyze metrics for every active SNS. Once users have configured CloudWatch for Amazon SNS, they can gain better insight into the performance of their Amazon SNS topics, push notifications, and SMS deliveries.'

                },
                {
                    text: 'Where can a user find information about prohibited actions on the AWS infrastructure?',
                    choices: [
                        { id: 'a', text: 'AWS Trusted Advisor', selectedChoice: null },
                        { id: 'b', text: 'AWS Identity and Access Management (IAM)', selectedChoice: null },
                        { id: 'c', text: 'AWS Billing Console', selectedChoice: null },
                        { id: 'd', text: 'AWS Acceptable Use Policy', selectedChoice: null },
                    ],
                    correctAnswear: 'd',
                    explanation: 'The AWS Acceptable Use Policy provides information regarding prohibited actions on the AWS infrastructure.'

                },
            ]
        }
    },
    methods: {
        startCountdown() {
            let countdownInterval = setInterval(() => {
                if (this.countdown > 0) {
                    this.countdown--;
                } else {
                    clearInterval(countdownInterval);
                    this.statraTimer();
                }
            }, 1000);
            this.$emit('changeStatus', true);
        },
        statraTimer() {
            this.countTimerInterval = setInterval(() => {
                if (this.timer > 0) {
                    this.timer--;
                } else {
                    this.clickNext()
                }
            }, 1000)
        },
        getCheckedChoices() {
            const checkedChoices = this.questions[this.currentQuestion].choices.filter(choice => choice.selectedChoice)
                if (checkedChoices.length > 0) {
                    return checkedChoices.map(choice => choice.id)
                } else {
                    this.checkedAnswear.push('')
                }
        },
        showNextButton() {
            if (this.currentQuestion <= 9) {
                this.hidbutton = false
            }
        },
        clickNext() {
            const checkedChoices = this.getCheckedChoices()
            this.checkedAnswear.push(checkedChoices)
            clearInterval(this.countTimerInterval);
            this.hidbutton = true
            if (this.currentQuestion < 9) {
                this.timer = 10
                this.statraTimer()
                this.currentQuestion++;
            } else {
                this.hidediv = true
                this.checkAnswer()
                this.$emit('changeStatus', false, this.score, this.newQuestions);
            }
        },
        checkAnswer() {
            this.score = 0;
            let i=0;
            this.questions.forEach(question => {
                console.log(question.correctAnswear)
                if (question.correctAnswear === this.checkedAnswear[i]) {
                    this.score++;
                } else {
                    const fullQuestion = {
                        question: question,
                        selectedChoices: this.checkedAnswear[i],
                    };
                    this.newQuestions.push(fullQuestion);
                }
                i++
            });
        },
    },
    mounted() {
        this.startCountdown();
    }
}
</script>
<template>
    <div v-if="this.countdown > 0" class="w-full absolute top-0 left-0 h-screen bg-black  flex justify-center items-center">
        <div class="flex justify-center items-center text-[120px]">
            <h1 class="text-white font-bold ">{{ countdown }}</h1>
        </div>
    </div>
    <div v-else>
        <div>
            <div class="">
                <div class="flex justify-center items-center w-full">
                    <div class="bg-gray-300 w-24 h-24  rounded-full"></div>
                    <div class="flex items-center justify-center text-white absolute bg-zinc-700 rounded-full w-20 h-20">
                        <p class="text-white font-bold" id="date-crono">{{ this.timer }}</p>
                    </div>
                </div>
                <p class="text-center">Question <span class="curent-question"> {{ this.currentQuestion + 1 }}</span > / <span
                        class="total-question">10</span></p>
            </div>
            <div class="bg-gray-700 w-4/5 h-2 mt-14  m-auto rounded">
                <div class="bg-yellow-500 h-full rounded "></div>
            </div>
            <h5 class="mb-2 mt-16 text-center text-xl font-bold  dark:text-white">
                {{ questions[this.currentQuestion].text }}
            </h5>
            <div
                class="content-card w-full mt-20   grid xl:grid-cols-4 lg:grid-cols-3 md:grid-cols-2 justify-items-center gap-x-16 ">
                <label @click="showNextButton" :for="choice.id" v-for="choice in questions[this.currentQuestion].choices"
                    :key="choice.id"
                    class="h-[100px] w-[300px]  relative flex items-center justify-center cursor-pointer  my-2  mx-2 max-w-sm p-6 bg-gray-800   rounded-lg shadow-md hover:bg-indigo-900">
                    <p class="text-white text-center">{{ choice.text }}</p>
                    <input class="absolute left-1 top-1" type="checkbox" :id="choice.id" :value="choice.id"
                        v-model="choice.selectedChoice">
                </label>
            </div>

        </div>
        <div v-if="!this.hidediv">
            <button v-if="!this.hidbutton" @click="clickNext"
                class="flex border-dashed  border-2 border-blue-700 bg-slate-600 rounded-md px-3 py-2 my-3 text-white">Next</button>
        </div>

    </div>
</template>
<style>
input[type="checkbox"] {
    appearance: none;
    -webkit-appearance: none;
    /* Remove the default checkbox appearance */
    -moz-appearance: none;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    border: 2px solid #e9e9e9;
    outline: none;
    transition: background-color 0.2s;
}

input[type="checkbox"]:checked {
    background-color: #4000d4;
}

input[type="checkbox"]:checked:after {
    content: '\2713';
    color: white;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
</style>
