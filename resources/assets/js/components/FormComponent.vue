// FormComponent.vue

<template>
    <div class="col-md-4">
        <form @submit.prevent="saveTweet">
            <div class="form-group">
                <textarea 
                    class="form-control" 
                    rows="8" cols="8" 
                    maxlength="130"
                    v-model="body"
                    required>
                </textarea>
            </div>
            <div class="form-group">
                <button class="btn btn-primary">
                    Tweet
                </button>
            </div>
        </form>        
    </div>
</template>
<script>
export default {
    data() {
        return {
            body: ''
        }
    },
    methods: {
        saveTweet() {
            axios.post('http://localhost:8888/laratwitter/public/tweet/save', {body: this.body}).then(res => {
                console.log(res.data);
            }).catch(e => {
                console.log(e);
            });
            
        }
    }
}
</script>


<template>
    <div class="col-md-4">
        <form @submit.prevent="saveTweet">
            <div class="form-group">
                <textarea 
                    class="form-control" 
                    rows="8" cols="8" 
                    maxlength="130"
                    v-model="body"
                    >
                </textarea>
            </div>
            <div class="form-group">
                <button class="btn btn-primary">
                    Tweet
                </button>
            </div>
        </form>        
    </div>
</template>
<script>
import Event from '../event.js';
export default {
    data() {
        return {
            body: '',
            postData: {}
        }
    },
    methods: {
        saveTweet() {
            axios.post('http://localhost:8888/laratwitter/public/tweet/save', {body: this.body}).then(res => {
                this.postData = res.data;
                console.log(res.data);
                Event.$emit('added_tweet', this.postData);
            }).catch(e => {
                console.log(e);
            });
            this.body = '';
        }
    }
}
</script>