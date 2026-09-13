<script setup>
import axios from 'axios';
import { ref } from 'vue';
import { useRouter } from "vue-router";
const moods = ref(['Happy', 'Sad', 'Angry']);
const subject = ref('');
const entry = ref('');
const mood = ref('');


// Add Code Here
const router = useRouter();

//need function to send post to backend
async function submitPost(){
  if (!subject.value || !entry.value || !mood.value){
    alert("Please fill out all required fields.");
    return;
  }

  try{
    // sendss Post request matching controller
    await axios.post("http://localhost:8000/posts",{
      subject: subject.value,
      entry: entry.value,
      mood: mood.value
    });

    // Reset input fields
    subject.value ="";
    entry.value="";
    mood.value="";

    //Redirect back to main page after creation
    router.push('/ViewPosts/');
    } catch(error){
      console.error('Failed to create post');
      alert(error.response?.data?.error || "Failed to submit post");
    }
  }

</script>

<template>
    <div class="table m-2">
        <h3>Add a New Blog Post</h3>

        Subject: <input type='text' size='30' v-model='subject' required>
        <br>

        Entry: <br>
        <textarea name='entry' cols='80' rows='5' v-model='entry' required></textarea>
        <br>

        <!-- TODO: Build a dropdown list here for selecting the mood -->
        <label>Mood:  </label>
        <select v-model="mood">
          <option value="" disabled>Choose Mood</option>
              <option v-for="m in moods" :key="m" :value="m">{{ m }}</option>
          </select>
        <br>

        <br>
        <button @click="submitPost">Submit New Post</button>

        <hr>
        <RouterLink to="/ViewPosts/">Click  here to return to Main Page</RouterLink>

    </div>
</template>

