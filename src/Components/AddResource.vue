<template>
    <base-dialog v-if='inputIsInvalid' title="Invalid Input" @close='confirmError'>
        <template #default>
            <p>Unfortunately, at least one input is invalid.</p>
            <p>check all inputs, and make sure you enter at least a few characters into each input field</p>
        </template>

        <template #actions>
            <base-button @click='confirmError'>Okay</base-button>
        </template>
    </base-dialog>

    <base-card>
        <form @submit.prevent="submitForm">
            <div class="form-control">
                <label for="title">Title</label>
                <input  id="title" type="text" v-model="enteredTitle">
            </div>

            <div class="form-control">
                <label for="description">Description</label>
                <textarea id="description"  rows="3" v-model="enteredDescription"></textarea>
            </div>

            <div class="form-control">
                <label for="link">Link</label>
                <input  id="link" type="url" v-model="enteredLink">
            </div>

            <div>
                <base-button >Submit</base-button>
            </div>
        </form>
    </base-card>
</template>
 
<script>
export default {
    inject:['addResource'],
    data(){
        return {
            enteredTitle:'',
            enteredDescription:'',
            enteredLink:'',
            inputIsInvalid:false,
        }
    },

    methods:{
        submitForm(){
            if (this.enteredTitle.trim==='' || this.enteredDescription==='' || this.enteredLink===''){
                this.inputIsInvalid=true
            }
            else{
                this.addResource(this.enteredTitle, this.enteredDescription, this.enteredLink)
            }
            
        },

        confirmError(){
            this.inputIsInvalid=false;
        }
    }
}
</script>


<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
