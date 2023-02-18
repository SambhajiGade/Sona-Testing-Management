<template>
  <!-- <v-container> -->

  <v-app>
    <v-card color="#90CAF9" width="400">
      <v-card-title> Welcome to Sona Testing </v-card-title>

      <v-card-text class="pb-2">
        <v-text-field label="Email" solo></v-text-field>

        <v-text-field
          :append-icon="show3 ? 'mdi-eye' : 'mdi-eye-off'"
          :rules="[rules.required, rules.min]"
          :type="show3 ? 'text' : 'password'"
          name="input-10-2"
          label="Password"
          hint="At least 8 characters"
          solo
          class="input-group--focused"
          @click:append="show3 = !show3"
        ></v-text-field>
      </v-card-text>

      <v-divider class="mx-4"></v-divider>

      <v-card-text class="text-center text-h6">
        <b>OR</b>
      </v-card-text>

      <v-card-text class="text-center">
        <img src="../assets/google.png" alt="" width="60" height="50" />
        <img src="../assets/link.png" alt="" width="60" height="50" />
      </v-card-text>

      <v-card-actions class="justify-center">
        <v-btn
          flat
          dark
          color="blue darken-1 text-white px-10 mb-5"
          to="/Home/"
        >
          Sign In
        </v-btn>
      </v-card-actions>
    </v-card>

    <!-- <v-data-table :headers="headers" :items="desserts" sort-by="calories" item-key="name" show-select>
      <template v-for="(col, i) in filters" v-slot:[`header.${i}`]="{ header }">
        <div style="display: inline-block; padding: 16px 0;">{{ header.text }}</div>
        <div style="float: right; margin-top: 8px">
          <v-menu :close-on-content-click="false" :nudge-width="200" offset-y transition="slide-y-transition" left fixed style="position: absolute; right: 0">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="indigo" icon v-bind="attrs" v-on="on">
                <v-icon small 
                  :color="activeFilters[header.value].length < filters[header.value].length ? 'red' : 'default'">
                  mdi-filter-variant
                </v-icon>
              </v-btn>
            </template>
            <v-list flat dense class="pa-0">
              <v-list-item-group multiple v-model="activeFilters[header.value]" class="py-2">
                <template v-for="(item, i) in filters[header.value]" >
                  <v-list-item :key="`item-${i}`" :value="item" :ripple="false">
                    <template v-slot:default="{ active, toggle }">
                      <v-list-item-action>
                        <v-checkbox :input-value="active" :true-value="item"
                          @click="toggle" color="primary" dense></v-checkbox>
                      </v-list-item-action>
                      <v-list-item-content>
                        <v-list-item-title v-text="item"></v-list-item-title>
                      </v-list-item-content>
                    </template>
                  </v-list-item>
                </template>
              </v-list-item-group>
              <v-divider></v-divider>
              <v-btn text block @click="toggleAll(header.value)">Toggle all</v-btn>
              <v-btn text block @click="clearAll(header.value)">Clear all</v-btn>
            </v-list>
          </v-menu>
        </div>
      </template>
      
      
       <template v-for="(col1, i) in filters1" v-slot:[`header.${i}`]="{ header }">
        <div style="display: inline-block; padding: 16px 0;">{{ header.text }}</div>
        <div style="float: right; margin-top: 8px">
          <v-menu :close-on-content-click="false" :nudge-width="200" offset-y transition="slide-y-transition" left fixed style="position: absolute; right: 0">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="indigo" icon v-bind="attrs" v-on="on">
                <v-icon small 
                  :color="activeFilters1[header.value].length < filters[header.value].length ? 'red' : 'default'">
                  mdi-filter-variant
                </v-icon>
              </v-btn>
            </template>
            <v-list flat dense class="pa-0">
              <v-list-item-group multiple v-model="activeFilters1[header.value]" class="py-2">
                <template v-for="(item, i) in filters1[header.value]" >
                  <v-list-item :key="`item-${i}`" :value="item" :ripple="false">
                    <template v-slot:default="{ active, toggle }">
                      <v-list-item-action>
                        <v-checkbox :input-value="active" :true-value="item"
                          @click="toggle" color="primary" dense></v-checkbox>
                      </v-list-item-action>
                      <v-list-item-content>
                        <v-list-item-title v-text="item"></v-list-item-title>
                      </v-list-item-content>
                    </template>
                  </v-list-item>
                </template>
              </v-list-item-group>
              <v-divider></v-divider>
              <v-btn text block @click="toggleAll1(header.value)">Toggle all</v-btn>
              <v-btn text block @click="clearAll1(header.value)">Clear all</v-btn>
            </v-list>
          </v-menu>
        </div>
      </template>
      <template v-slot:header="{ props: { headers } }">
        <thead>
          <tr>
            <th :colspan="headers.length">
              This is a header
            </th>
          </tr>
        </thead>
      </template>
      <template v-slot:top>
        <v-toolbar flat color="white">
          <v-toolbar-title>My CRUD</v-toolbar-title>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>
          <v-dialog v-model="dialog1" max-width="500px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="primary" dark class="mb-2" v-bind="attrs" v-on="on">New Item</v-btn>
            </template>
            <v-card>
              <v-card-title>
                <span class="headline">{{ formTitle }}</span>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.name" label="Dessert name"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.calories" label="Calories"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.fat" label="Fat (g)"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.carbs" label="Carbs (g)"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.protein" label="Protein (g)"></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
                <v-btn color="blue darken-1" text @click="save">Save</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:[`item.actions`]="{ item }">
        <v-icon small class="mr-2" @click="editItem(item)">
          mdi-pencil
        </v-icon>
        <v-icon small @click="deleteItem(item)">
          mdi-delete
        </v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize">Reset</v-btn>
      </template>
    </v-data-table> -->
    <!-- <v-select
                    v-model="asd1"
                    :items="DTList"
                    label="Select"
                    item-title="text"
    item-value="value"
                    persistent-hint
                    return-object
                    single-line
                   
                    required
                  >
                  </v-select>
                <v-text-field
                v-model="s.asd"
                >
                    
                </v-text-field> -->

  </v-app>
  <!-- </v-container> -->
</template>

<style>
html {
  overflow-y: auto;
}
.v-list--dense .v-list-item, .v-list-item--dense {
  min-height: 20px !important;
  height: 2rem;
}

.v-application--is-ltr .v-list-item__action:first-child, .v-application--is-ltr .v-list-item__icon:first-child {
  margin-right: .5rem !important;
}
</style>

<!-- REQUIRED SCRIPTS  -->

<script>
// import * as firebase from "firebase/app";

// import {
//   getStorage,
//   ref,
//   uploadBytesResumable,
//   getDownloadURL,
// } from "firebase/storage";

// const firebaseConfig = {
//   apiKey: "AIzaSyBsAdm3QQTHlmwMihKSaXcEjcx-cwOeX8c",
//   authDomain: "project-360e7.firebaseapp.com",
//   projectId: "project-360e7",
//   storageBucket: "project-360e7.appspot.com",
//   messagingSenderId: "921356772970",
//   appId: "1:921356772970:web:362f876a5d94e3ae280c13",
// };

// Initialize Firebase
// firebase.initializeApp(firebaseConfig);

export default {
  data() {
    return {
      dialog1: true,
      items: [
        { title: "Institute" },
        { title: "Employer" },
        { title: "Student" },
      ],
      DTList: [
        // { text: "All", value: null },

        { text: "JJ01-A1B1", value: "JJ01-A1B1" },
        { text: "JJ01-A1B2", value: "JJ01-A1B2" },
        { text: "JJ01-A1B3", value: "JJ01-A1B3" },
        { text: "JJ01-A1B4", value: "JJ01-A1B4" },
      ],
      s:{

        asd:""
      },
      asd1:"",
      samurl: "",
      selectedfile: null,
      show3: false,
      uploadValue: 0,
      img1: null,
      password: "Password",
      rules: {
        required: (value) => !!value || "Required.",
        min: (v) => v.length >= 8 || "Min 8 characters",
      },


      dialog: false,
    name:"sam",
    filters: { 'name': [], 'calories': [], 'status': [] },
    filters1:{'fat':[],'carbs':[]},
    activeFilters: {},
    activeFilters1: {},
    desserts: [],
    editedIndex: -1,
    editedItem: {
      name: '',
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0,
    },
    defaultItem: {
      name: '',
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0,
    },
    };
  },
  created () {
    this.initialize()
  },

computed:{
  headers () {
      return [
        {
          text: 'Dessert (100g serving)',
          align: 'start',
          sortable: true,
          value: 'name',
          filter: value => {
            return this.activeFilters.name.includes(value);
          }
        },
        { text: 'Calories', value: 'calories',
          filter: value => {
            return this.activeFilters.calories.includes(value);
          }
        },
        { text: 'Status', value: 'status',
          filter: value => {
            return this.activeFilters.status.includes(value);
          }
        },
        { text: 'Fat (g)', value: 'fat',
          filter: value => {
            return this.activeFilters1.fat.includes(value);
          } 
        },
        { text: 'Carbs (g)', value: 'carbs' ,
          filter: value => {
            return this.activeFilters1.carbs.includes(value);
          }
        },
        { text: 'Protein (g)', value: 'protein' },
        { text: 'Actions', value: 'actions', sortable: false },
      ]
    },
    formTitle () {
      return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
    },
  },

  watch: {
    asd1(val){
      console.log("value is : ",val);
      this.s.asd=val.value
    }
    ,
    dialog (val) {
      val || this.close()
    },
    /*filters: {
      deep: true,
      handler(val) {
        console.log(val)
      }
    }*/
},

  methods: {


  //   initialize () {
  //     this.desserts = [
  //       {
  //         name: 'Frozen Yogurt',
  //         calories: 159,
  //         fat: 6.0,
  //         carbs: 24,
  //         protein: 4.0,
  //         status: 'DIET'
  //       },
     
  //        {
  //         name: 'Frozen Yogurt',
  //         calories: 145,
  //         fat: 46.0,
  //         carbs: 244,
  //         protein: 44.0,
  //         status: 'DIET'
  //       },
  //          {
  //         name: 'Frozen Yogurt',
  //         calories: 19,
  //         fat: 64.0,
  //         carbs: 244,
  //         protein: 44.0,
  //         status: 'DIET'
  //       },
  //       {
  //         name: 'Ice cream sandwich',
  //         calories: 237,
  //         fat: 9.0,
  //         carbs: 37,
  //         protein: 4.3,
  //         status: 'NO DIET'
  //       },
  //       {
  //         name: 'Eclair',
  //         calories: 262,
  //         fat: 16.0,
  //         carbs: 23,
  //         protein: 6.0,
  //         status: 'DIET'
  //       },
  //       {
  //         name: 'Cupcake',
  //         calories: 305,
  //         fat: 3.7,
  //         carbs: 67,
  //         protein: 4.3,
  //         status: 'NO DIET'
  //       },
  //       {
  //         name: 'Gingerbread',
  //         calories: 356,
  //         fat: 16.0,
  //         carbs: 49,
  //         protein: 3.9,
  //         status: 'DIET'
  //       },
  //       {
  //         name: 'Jelly bean',
  //         calories: 375,
  //         fat: 0.0,
  //         carbs: 94,
  //         protein: 0.0,
  //         status: 'NO DIET'
  //       },
  //       {
  //         name: 'Lollipop',
  //         calories: 392,
  //         fat: 0.2,
  //         carbs: 98,
  //         protein: 0,
  //         status: 'NO DIET'
  //       },
  //       {
  //         name: 'Honeycomb',
  //         calories: 408,
  //         fat: 3.2,
  //         carbs: 87,
  //         protein: 6.5,
  //         status: 'NO DIET'
  //       },
  //       {
  //         name: 'Donut',
  //         calories: 452,
  //         fat: 25.0,
  //         carbs: 51,
  //         protein: 4.9,
  //         status: 'DIET'
  //       },
  //       {
  //         name: 'KitKat',
  //         calories: 518,
  //         fat: 26.0,
  //         carbs: 65,
  //         protein: 7,
  //         status: 'NO DIET'
  //       },
  //     ];
  //      for (col in this.filters) {
  //       this.filters[col] = this.desserts.map((d) => { return d[col] }).filter(
  //         (value, index, self) => { return self.indexOf(value) === index }
  //       );
  //     }
  //      this.activeFilters = Object.assign({}, this.filters)
  //      for (col1 in this.filters1) {
  //       this.filters1[col1] = this.desserts.map((d1) => { return d1[col1] }).filter(
  //         (value1, index1, self1) => { return self1.indexOf(value1) === index1 }
  //       );
  //     }
  //     this.activeFilters1 = Object.assign({}, this.filters1)
     
     
     
    },
    
   
    
  //   toggleAll (col) {
  //     this.activeFilters[col] = this.desserts.map((d) => { return d[col] }).filter(
  //       (value, index, self) => { return self.indexOf(value) === index }
  //     )
  //   },
  //    toggleAll1 (col) {
  //     this.activeFilters1[col] = this.desserts.map((d) => { return d[col] }).filter(
  //       (value, index, self) => { return self.indexOf(value) === index }
  //     )
  //   },
    
  //   clearAll (col) {
  //     this.activeFilters[col] = []
  //   },
  //    clearAll1 (col) {
  //     this.activeFilters1[col] = []
  //   },

  //   editItem (item) {
  //     this.editedIndex = this.desserts.indexOf(item)
  //     this.editedItem = Object.assign({}, item)
  //     this.dialog = true
  //   },

  //   deleteItem (item) {
  //     const index = this.desserts.indexOf(item)
  //     confirm('Are you sure you want to delete this item?') && this.desserts.splice(index, 1)
  //   },

  //   close () {
  //     this.dialog = false
  //     this.$nextTick(() => {
  //       this.editedItem = Object.assign({}, this.defaultItem)
  //       this.editedIndex = -1
  //     })
  //   },

  //   save () {
  //     if (this.editedIndex > -1) {
  //       Object.assign(this.desserts[this.editedIndex], this.editedItem)
  //     } else {
  //       this.desserts.push(this.editedItem)
  //     }
  //     this.close()
  //   },
    
  // },



    // filechange(event) {
    //   this.selectedfile = event.target.files[0];
    //   console.log("Selected file : ", this.selectedfile);
    //   console.log("Event : ", event);
    // },

    // uploadfile() {
    //   const storage = getStorage();

    //   const metadata = {
    //     contentType: "image/jpeg",
    //   };

    //   // Create a reference to 'mountains.jpg'
    //   const mountainsRef = ref(storage, "data/" + this.selectedfile.name);

    //   const Task = uploadBytesResumable(
    //     mountainsRef,
    //     this.selectedfile,
    //     metadata
    //   );

    //   Task.on(
    //     "state_changed",
    //     (snapshot) => {
    //       // Get task progress, including the number of bytes uploaded and the total number of bytes to be uploaded
    //       const progress =
    //         (snapshot.bytesTransferred / snapshot.totalBytes) * 100;
    //       console.log("Upload is " + progress + "% done");
    //       switch (snapshot.state) {
    //         case "paused":
    //           console.log("Upload is paused");
    //           break;
    //         case "running":
    //           console.log("Upload is running");
    //           break;
    //       }
    //     },
    //     (error) => {
    //       // A full list of error codes is available at
    //       // https://firebase.google.com/docs/storage/web/handle-errors
    //       switch (error.code) {
    //         case "storage/unauthorized":
    //           // User doesn't have permission to access the object
    //           break;
    //         case "storage/canceled":
    //           // User canceled the upload
    //           break;

    //         // ...

    //         case "storage/unknown":
    //           // Unknown error occurred, inspect error.serverResponse
    //           break;
    //       }
    //     },
    //     () => {
    //       // Upload completed successfully, now we can get the download URL
    //       getDownloadURL(Task.snapshot.ref).then((downloadURL) => {
    //         this.samurl = downloadURL;
    //         console.log("File available at", downloadURL);
    //       });
    //     }
    //   );

    //   console.log("mountainsRef : ", mountainsRef);

    //   // console.log("app : ",app)
    //   console.log("firebase : ", firebase);
    // },
  // },
};
</script>
