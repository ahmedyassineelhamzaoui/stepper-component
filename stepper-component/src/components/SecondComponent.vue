<script>
export default{
    name:"Secondomponent",  
    data(){
        return{
            countdown: 3,   
            currentQuestion:0,
            hidbutton:true,
            isChecked: false,
            questions: [
                {
                    text: 'Why is AWS more economical than traditional data centers for applications with varying compute workloads?',
                    choices: [
                    { id: 'a', text: 'Amazon EC2 costs are billed on a monthly basis',selectedChoice: null },
                    { id: 'b', text: 'Users retain full administrative access to their Amazon EC2 instances',selectedChoice: null },
                    { id: 'c', text: 'Amazon EC2 instances can be launched on demand when needed',selectedChoice: null },
                    { id: 'd', text: 'Users can permanently run enough instances to handle peak workloads',selectedChoice: null },
                    ],
                },
                {
                    text: 'Which AWS service would simplify the migration of a database to AWS?',
                    choices: [
                    { id: 'a', text: 'AWS Storage Gateway' },
                    { id: 'b', text: 'AWS Database Migration Service (AWS DMS)',selectedChoice: null },
                    { id: 'c', text: 'Amazon EC2',selectedChoice: null },
                    { id: 'd', text: 'Amazon AppStream 2.0',selectedChoice: null },
                    ],
                },
                {
                    text: 'Which AWS offering enables users to find, buy, and immediately start using software solutions in their AWS environment?',
                    choices: [
                    { id: 'a', text: 'AWS Config',selectedChoice: null },
                    { id: 'b', text: 'AWS OpsWorks',selectedChoice: null },
                    { id: 'c', text: 'AWS SDK',selectedChoice: null },
                    { id: 'd', text: 'AWS Marketplace',selectedChoice: null },
                    ],
                },
                {
                    text: 'Which AWS networking service enables a company to create a virtual network within AWS?',
                    choices: [
                    { id: 'a', text: 'AWS Config',selectedChoice: null },
                    { id: 'b', text: 'Amazon Route 53',selectedChoice: null },
                    { id: 'c', text: 'AWS Direct Connect',selectedChoice: null },
                    { id: 'd', text: 'Amazon Virtual Private Cloud (Amazon VPC)',selectedChoice: null },
                    ],
                },
                {
                    text: 'Which of the following is an AWS responsibility under the AWS shared responsibility model?',
                    choices: [
                    { id: 'a', text: 'Configuring third-party applications',selectedChoice: null },
                    { id: 'b', text: 'Maintaining physical hardware',selectedChoice: null },
                    { id: 'c', text: 'Securing application access and data',selectedChoice: null },
                    { id: 'd', text: 'Managing guest operating systems',selectedChoice: null },
                    ],
                },
                {
                    text: 'Which component of the AWS global infrastructure does Amazon CloudFront use to ensure low-latency delivery?',
                    choices: [
                    { id: 'a', text: 'AWS Regions',selectedChoice: null },
                    { id: 'b', text: 'Edge locations',selectedChoice: null },
                    { id: 'c', text: 'Availability Zones',selectedChoice: null },
                    { id: 'd', text: 'Virtual Private Cloud (VPC)',selectedChoice: null },
                    ],
                },
                {
                    text: 'How would a system administrator add an additional layer of login security to a users AWSManagement Console?',
                    choices: [
                    { id: 'a', text: 'Use Amazon Cloud Directory',selectedChoice: null },
                    { id: 'b', text: 'Audit AWS Identity and Access Management (IAM) roles',selectedChoice: null },
                    { id: 'c', text: 'Enable multi-factor authentication',selectedChoice: null },
                    { id: 'd', text: 'Enable AWS CloudTrail',selectedChoice: null },
                    ],
                },
                {
                    text: 'Which service can identify the user that made the API call when an Amazon EC2 instance is terminated?',
                    choices: [
                    { id: 'a', text: 'AWS Trusted Advisor',selectedChoice: null },
                    { id: 'b', text: 'AWS CloudTrail',selectedChoice: null },
                    { id: 'c', text: 'AWS X-Ray',selectedChoice: null },
                    { id: 'd', text: 'AWS Identity and Access Management (AWS IAM)',selectedChoice: null },
                    ],
                },
                {
                    text: '"Which service would be used to send alerts based on Amazon CloudWatch alarms?',
                    choices: [
                    { id: 'a', text: 'Amazon Simple Notification Service (Amazon SNS)',selectedChoice: null },
                    { id: 'b', text: 'AWS CloudTrail',selectedChoice: null },
                    { id: 'c', text: 'AWS Trusted Advisor',selectedChoice: null },
                    { id: 'd', text: 'Amazon Route 53',selectedChoice: null },
                    ],
                },
                {
                    text: 'Where can a user find information about prohibited actions on the AWS infrastructure?',
                    choices: [
                    { id: 'a', text: 'AWS Trusted Advisor',selectedChoice: null },
                    { id: 'b', text: 'AWS Identity and Access Management (IAM)',selectedChoice: null },
                    { id: 'c', text: 'AWS Billing Console',selectedChoice: null },
                    { id: 'd', text: 'AWS Acceptable Use Policy',selectedChoice: null },
                    ],
                },
            ]
        }
    },
    methods:{
        startCountdown() {
            let countdownInterval = setInterval(() => {
            if(this.countdown > 0) {
                this.countdown--;
            }else
            {
                clearInterval(countdownInterval);
            }
            }, 1000);
            this.$emit('changeStatus',false);
        },
        showNext() {
            this.hidbutton=false
        },
        onChoiceSelected() {
            if(this.currentQuestion<9){
                    this.hidbutton=true
                    this.isChecked = false;
                    this.currentQuestion++;
            }else{
                    this.$emit('changeStatus',true);
                    this.hidbutton=true
            }
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
        <h5  class="mb-2 text-center text-xl font-bold  dark:text-white">
            {{ questions[this.currentQuestion].text }}
        </h5>
        <div class="content-card w-full mt-20   grid xl:grid-cols-4 lg:grid-cols-3 md:grid-cols-2 justify-items-center gap-x-16 ">
            <label @click="showNext" :for="choice.id" v-for="choice in questions[this.currentQuestion].choices" :key="choice.id" class="h-[100px] w-[300px]  relative flex items-center justify-center cursor-pointer  my-2  mx-2 max-w-sm p-6 bg-gray-800   rounded-lg shadow-md hover:bg-indigo-900">
                <p class="text-white text-center" >{{ choice.text }}</p>
                <input class="absolute left-1 top-1" type="checkbox" :id="choice.id" :value="choice.id"  v-model="choice.selectedChoice">
            </label>
        </div>

    </div>
    <button  v-if="!hidbutton" @click="onChoiceSelected" class="flex border-dashed border-2 border-blue-700 bg-slate-600 rounded-md px-3 py-2 my-3 text-white">Next</button>
    </div> 
</template>
<style>
input[type="checkbox"]{
    appearance: none;
    -webkit-appearance: none; /* Remove the default checkbox appearance */
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
