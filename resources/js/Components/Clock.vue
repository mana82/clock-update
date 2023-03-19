<template>
    
    <div v-if="isPageLoaded">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-2 lg:gap-8 p-6 lg:p-8 bg-white min-h-screen">
            
            <div>
                <div class="flex items-center">
                    <div class="text-8xl font-semibold text-red-400">
                        <span class="">{{ Hours }}</span>
                        <span>:</span>
                        <span class="">{{ Minutes }}</span>
                        <span>:</span>
                        <span class="">{{ Seconds }}</span>
                    </div>
                </div>
                <div class="flex items-center text-gray-900">
                    <p @click="visible = !visible" class="cursor-pointer">Change Time</p>
                    <input type="time" v-model="selectedTime" @change="updateSelectedTime" v-if="visible">
                </div>
            </div>

        </div>
    </div>
</template>


<script>

export default {
    data () {
        return {
            Hours: 0,
            Minutes: 0,
            Seconds: 0,
            isPageLoaded: false
        }
    },
    mounted(){
        setInterval(() => this.setClock(), 1000)
    },
    methods: {
        // format time to show with '0'...
        formatTime : time => (time <= 9 ? "0" + time : time),
        setClock() {
            const date = new Date();
            let Hours = date.getHours();
            let Minutes = date.getMinutes();
            let Seconds = date.getSeconds();

            // check user already set a time...
            if(localStorage.getItem('storedTimeDifference')){
                // get user selected time defference in milisecond...
                const userTime = localStorage.getItem('storedTimeDifference');
                // set date  object with user select time defference...
                date.setTime(date.getTime() + (userTime * 1000));

                this.Hours = this.formatTime(date.getHours());
                this.Minutes = this.formatTime(date.getMinutes());
                this.Seconds = this.formatTime(date.getSeconds());

            }else{
                // user not set time so we show system time...
                this.Hours = this.formatTime(Hours);
                this.Minutes = this.formatTime(Minutes);
                this.Seconds = this.formatTime(Seconds);
            }
            
            this.isPageLoaded = true;
        
        },
        updateSelectedTime() {
            
            let now = new Date();
            let userSetTime = new Date();

            // split user selected time to houres, min and sec...
            let timeParts = this.selectedTime.split(":");

            userSetTime.setHours(+timeParts[0]);
            userSetTime.setMinutes(+timeParts[1]);
            //userSetTime.setSeconds(+timeParts[2]);
            
            // set user selected time defference in milisecond...
            let timeDifference = Math.round((userSetTime.getTime() - now.getTime()) / 1000);
            // set user selected time defference to local storage...
            localStorage.setItem('storedTimeDifference', timeDifference);
      }
    }
};
</script>

<style lang="css" scoped>

</style>
