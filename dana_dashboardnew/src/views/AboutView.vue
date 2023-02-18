<template>
  
  <v-data-table
    :headers="headers"
    :items="desserts"
    sort-by="calories"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title>Geometeric Parameters</v-toolbar-title>
        
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="1000px">
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" class="mx-auto" width="200px" v-bind="attrs" v-on="on">
              New Item
            </v-btn>
          </template>
          <v-card>
            <v-card-title class="pa-md-4 mx-lg-auto">
              <span class="text-h5" style="margin-left: 400px">{{
                formTitle
              }}</span>
            </v-card-title>
            <v-col cols="12" sm="6" ms="8" style="margin-left: 250px">
              <v-text-field
                v-model="editedItem.name"
                label="Project Name "
                outlined
              ></v-text-field>
            </v-col>
            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.calories"
                      label="Gear Pair"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.fat"
                      label="Model"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Design"
                      outlined
                    ></v-text-field>
                  </v-col>
                  
                </v-row>
                <v-divider></v-divider>
              </v-container>
              <span class="text-h5">Gear Parameters</span>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.calories"
                      label="Number of Teeth"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.fat"
                      label="Raw Material Gear"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Module"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Pressure Angle[Deg.]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="P.C.D[mm]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Pitch Angle[Deg.]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Face Angle[Deg.]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Root Angle[Deg.]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Outer Dia[mm]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="M.D.[mm]"
                      outlined
                    ></v-text-field>
                  </v-col>
                </v-row>
                <v-divider></v-divider>
              </v-container>
              <span class="text-h5">Pinion Parameters</span>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.calories"
                      label="Number of Teeth"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.fat"
                      label="Raw Material Pinion"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="P.C.D.[mm]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Pitch Angle[Deg.]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Face Angle[Deg.]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Pitch Angle[Deg.]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Face Angle[Deg.]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Root Angle[Deg.]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="Outer Dia[mm]"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.carbs"
                      label="M.D.[mm]"
                      outlined
                    ></v-text-field>
                  </v-col>
                </v-row>
                <v-divider></v-divider>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="close"> Cancel </v-btn>
              <v-btn color="blue darken-1" text @click="save"> Save </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5"
              >Are you sure you want to delete this item?</v-card-title
            >
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete"
                >Cancel</v-btn
              >
              <v-btn color="blue darken-1" text @click="deleteItemConfirm"
                >OK</v-btn
              >
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:[`item.actions`]="{ item }">
      <v-icon small class="mr-2" @click="editItem(item)"> mdi-pencil </v-icon>
      <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn color="primary" @click="initialize"> Reset </v-btn>
    </template>
  </v-data-table>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: "Project ",
        align: "start",
        sortable: false,
        value: "name",
      },
      { text: "Grea Pair", value: "gearpair" },
      { text: "Model", value: "model" },
      { text: "Design", value: "carbs" },
      { text: "Number of Teeth", value: "carbs" },
      { text: "Raw Material Gear", value: "carbs" },
      { text: "Module", value: "carbs" },
      { text: "Pressure Angle[Deg.]", value: "carbs" },
      { text: "P.C.D[mm]", value: "carbs" },
      { text: "Pitch Angle[Deg.]", value: "carbs" },
      { text: "Face Angle[Deg.]", value: "carbs" },
      { text: "Root Angle[Deg.]", value: "carbs" },
      { text: "Outer Dia[Deg.]", value: "carbs" },
      { text: "M.D.[mm]", value: "carbs" },
      { text: "Number of Teeth", value: "carbs" },
      { text: "Raw Material Pinion", value: "carbs" },
      { text: "P.C.D", value: "carbs" },
      { text: "Pitch Angle", value: "carbs" },
      { text: "Face Angle", value: "carbs" },
      { text: "Root Angle", value: "carbs" },
      { text: "Outer Dia", value: "carbs" },
      { text: "M.D.", value: "carbs" },
      { text: "Sph.Radius", value: "carbs" },
      { text: "Bore Dia", value: "carbs" },

      { text: "Actions", value: "actions", sortable: false },
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      name: "",
      gearpair: "",
      fat: "",
      carbs: "",
      protein: "",
    },
    defaultItem: {
      name: "",
      gearpair: "",
      fat: "",
      carbs: "",
      protein: "",
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.desserts = [
        {
          name: "JJ01",
          gearpair: "JJ01A1B1",
          model: 6.0,
          carbs: 24,
          protein: 4.0,
        },
        {
          name: "JJ02",
          gearpair:  "JJ01A1B2",
          model: 9.0,
          carbs: 37,
          protein: 4.3,
        },
        {
          name: "JJ03",
          gearpair:  "JJ01A1B3",
          model: 16.0,
          carbs: 23,
          protein: 6.0,
        },
        {
          name: "JJ04",
          gearpair:  "JJ01A1B4",
          model: 3.7,
          carbs: 67,
          protein: 4.3,
        },
        {
          name: "JJ05",
          gearpair:  "JJ01A1B5",
          model: 16.0,
          carbs: 49,
          protein: 3.9,
        },
        {
          name: "JJ06",
          gearpair:  "JJ01A1B6",
          model: 0.0,
          carbs: 94,
          protein: 0.0,
        },
        {
          name: "JJ07",
          gearpair:  "JJ01A1B7",
          model: 0.2,
          carbs: 98,
          protein: 0,
        },
        {
          name: "JJ08",
          gearpair:  "JJ01A2B1",
          model: 3.2,
          carbs: 87,
          protein: 6.5,
        },
        {
          name: "JJ09",
          gearpair:  "JJ01A3B1",
          model: 25.0,
          carbs: 51,
          protein: 4.9,
        },
        {
          name: "JJ10",
          gearpair:  "JJ01A4B1",
          model: 26.0,
          carbs: 65,
          protein: 7,
        },
      ];
    },

    editItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.desserts.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.desserts[this.editedIndex], this.editedItem);
      } else {
        this.desserts.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>
