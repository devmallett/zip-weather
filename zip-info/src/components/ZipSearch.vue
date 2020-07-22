<template>
    <ion-grid>
        <form @submit="onSubmit" >
            <ion-col>
                <ion-item>
                    <ion-label>
                        Zipcode: 
                    </ion-label>
                    <ion-input :value="zip" @input="zip= $event.target.value"  placeholder="enter" name="zip"></ion-input>
                </ion-item>
            </ion-col>
            <ion-col>
                <ion-button type="submit" color="primary" expand="block">Find</ion-button>
            </ion-col>
        </form>


    </ion-grid>
 
</template>

<script>
export default {
    name: "ZipSearch",
    // Binding Zip to input
    data() {
      return{
          zip: ""
      }  
    },
    methods: {
        onSubmit(e) {
            e.preventDefault();

            // Zip Regex
            const isValidZip = /(^\d{5}$)|(^\d{5}-\d{4}$)/.test(this.zip);
            // console.log(this.zip);
            if (!isValidZip) {
                this.showAlert();
                this.zip="";
            }else{
                this.$emit("get-zip", this.zip);
                this.zip="";
            }

        },
        showAlert(){
            return this.$ionic.alertController
            .create({
                header: "Enter ZipCode",
                message: "Enter a valid zip code",
                buttons: ["OK"]
            })
            .then( a => a.present())
        }
    }

}
</script>
