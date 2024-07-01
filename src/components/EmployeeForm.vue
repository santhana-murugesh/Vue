<template>
    <div id="employee-form">
        <form @submit.prevent="handleSubmit">
            <Label>Employee Name</Label>
            <input type="text" 
            v-model= "employee.name"
             :class="{ 'has-error': submitting && invalidName }"
            @focus="clearStatus"
            @keypress="clearStatus"/>
            <Label>Employee Email</Label>
            <input type="text"
                v-model="employee.email"
               :class="{ 'has-error': submitting && invalidEmail }"
               @focus="clearStatus"
               @keypress="clearStatus" />

               <p v-if="submitting&&error" class="error-msg">please fill out all the required fields! </p>
               <p v-if="success" class="error-suc"> employee successfully added</p>
            <button>Add Employee</button>
        </form>
    </div>
</template>
<script>
export default {
    name:'employee-form',
    data(){
        return{
            submitting:false,
            success:false,
            error:false,
            employee : {
                id:'',
                name:'',
                email:''
            }
        }
       
    },


    methods:{
        handleSubmit(){
            this.submitting=true;
            this.clearStatus();

        if(this.invalidName||this.invalidEmail){
            this.error=true;
            return;
        }
            this.$emit('add:employee',this.employee)
            this.employee = {
                name:'',
                email:''
            };
            this.success=true;
            this.error=false;
            this.submitting=false;
        },
        
        clearStatus(){
            this.success=false;
            this.error=false;
        }
    },

    computed: {
        invalidName(){
            return this.employee.name==='';
        },
        invalidEmail(){
            return this.employee.email==='';
        }
}
}



</script>
<style scoped>
form {
  margin-bottom: 2rem;
}
.has-error {
    border: 1px solid red;
  }
  
  .error-msg {
    color: red;
    font-weight: 500px;
  }
  
  .error-suc{
    color: green;
  }

</style>
