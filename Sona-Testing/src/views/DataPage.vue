<template>
  <v-app>
    <div></div>

    <div class="text-left ml-10 mb-5">
      <v-dialog v-model="dialog" width="900">
        <template v-slot:activator="{ on, attrs }">
          <v-row class="mt-8 ml-8">
            <v-btn color="primary" class="white--text" v-bind="attrs" v-on="on">
              <v-icon dark>mdi-plus</v-icon>Add
            </v-btn>

            <v-btn
              color="primary"
              class="white--text ml-3"
              @click="edit(selected1)"
              >EDIT</v-btn
            >
            <v-col cols="2" class="pa-0">
              <v-select
                :items="DTList"
                v-model="DTFilterValue"
                label="Gear Pair"
                class="pa-0 ml-3"
                @change="Selecteditm1"
              ></v-select>
            </v-col>
            <v-btn
              color="primary"
              class="white--text ml-3"
              @click="dash2()"
              :disabled="disableb"
              >Search</v-btn
            >

            <v-btn color="primary" class="white--text ml-3" to="/Home"
              >HOME</v-btn
            >
          </v-row>

          <!-- <v-row> -->
            <!-- <v-col cols="auto">
              <p align="center">Gear Pair</p>
              <div v-for="item in GearPair" :key="item" class="ma-0">
                <v-checkbox
                  v-model="SortedGearPair"
                  :label="item.text"
                  :value="item.value"
                  class="ma-0"
                ></v-checkbox>
              </div>
            </v-col> -->

            <!-- <v-col cols="auto">
              <p align="center">Differential Torque</p>

              <div v-for="item in items1" :key="item" class="ma-0">
                <v-checkbox
                  v-model="SortedDT"
                  :label="item.text"
                  :value="item.value"
                  class="ma-0"
                ></v-checkbox>
              </div>
            </v-col> -->

            <!-- <v-col cols="auto">
              <p align="center">Application</p>

              <div v-for="item in Application" :key="item" class="ma-0">
                <v-checkbox
                  v-model="SortedApplication"
                  :label="item.text"
                  :value="item.value"
                  class="ma-0"
                ></v-checkbox>
              </div>
            </v-col> -->

            <!-- <v-col cols="auto">
              <p align="center">Steps</p>

              <div v-for="item in items" :key="item" class="ma-0">
                <v-checkbox
                  v-model="SortedSteps"
                  :label="item.text"
                  :value="item.value"
                  class="ma-0"
                ></v-checkbox>
              </div>
            </v-col> -->

            <!-- <v-col cols="auto">
              <p align="center">Fields</p>

              <div v-for="item in SortList" :key="item" class="ma-0">
                <v-checkbox
                  v-model="SortedValue"
                  :label="item.text"
                  :value="item"
                  class="ma-0"
                ></v-checkbox>
              </div>
            </v-col> -->
          <!-- </v-row> -->

          <!-- <v-row> -->
            <!-- <v-col
              cols="3"
              class="pa-0"
              style="
                display: flex;
                align-items: center;
                justify-content: center;
              "
              align="center"
            >
             <v-select
                :items="SortList"
                v-model="SortedValue"
                label="Select Field"
                class="pt-6 pb-2 ml-3"
               
                @change="SortField"
              ></v-select> -->
              <!-- <v-combobox
                v-model="SortedValue"
                :items="SortList"
                label="Select Fields"
                class="pt-6 pb-2 ml-3"
                @change="SortField"
                multiple
              ></v-combobox>

              <span align="center">Between </span> 
            </v-col> -->
            <!-- <v-col cols="1">
              <v-text-field
                v-model="greater"
                type="number"
                label="Greater than"
              ></v-text-field>
            </v-col> -->
            <!-- <v-col cols="1">
              <v-text-field
                v-model="less"
                type="number"
                label="Less than"
              ></v-text-field>
            </v-col> -->
          <!-- </v-row> -->
        </template>

        <v-card>
          <v-card-title class="text-h5 grey lighten-2">
            ADD DATA HERE
          </v-card-title>

          <v-divider></v-divider>

          <!-- ---------------------------------------------------------------------------------------------------- -->

          <v-card-text>
            <div ma-0>
              <v-row class="text-center" justify="center" align="center">
                <v-col cols="3">
                  <v-header class="font-weight-medium"> GEAR PAIR </v-header>
                </v-col>

                <v-col cols="3">
                  <v-select
                    v-model="postdata.Project"
                    :items="DTList"
                    label="Select"
                    persistent-hint
                    return-object
                    single-line
                    @change="Projectselected()"
                    :rules="[(v) => !!v || 'Gear Pair is required']"
                    required
                  >
                  </v-select>
                </v-col>
              </v-row>

              <v-row
                class="text-center"
                justify="center"
                align="center"
                pa-0
                ma-0
                mt-0
              >
                <v-col cols="3" pa-0 ma-0>
                  <v-header class="font-weight-medium" pa-0 ma-0>
                    Differential Torque
                  </v-header>
                </v-col>

                <v-col cols="3" pa-0 ma-0>
                  <v-select
                    v-model="postdata.JJ01"
                    :items="items1"
                    label="Select"
                    persistent-hint
                    return-object
                    single-line
                    @change="DTselected()"
                    :rules="[(v) => !!v || 'Differential Torque is required']"
                    required
                  >
                  </v-select>
                </v-col>
              </v-row>

              <v-row class="text-center" justify="center" align="center">
                <v-col cols="3">
                  <v-header class="font-weight-medium"> Application </v-header>
                </v-col>

                <v-col cols="3">
                  <v-select
                    v-model="postdata.Column3"
                    :items="Application"
                    label="Select"
                    persistent-hint
                    return-object
                    single-line
                    @change="AppSelect()"
                    :rules="[(v) => !!v || 'Application is required']"
                    required
                  >
                  </v-select>
                </v-col>
              </v-row>

              <v-row class="text-center" justify="center" align="center">
                <v-col cols="3">
                  <v-header class="font-weight-medium" pa-0> STEPS </v-header>
                </v-col>

                <v-col cols="3">
                  <v-select
                    v-model="postdata.Report"
                    :items="items"
                    label="Select"
                    persistent-hint
                    return-object
                    single-line
                    @change="selectpost(postdata.Report)"
                    :rules="[(v) => !!v || 'Report is required']"
                    required
                  >
                  </v-select>
                </v-col>
              </v-row>
            </div>
            <br /><br />

            <v-container>
              <!-- --------------------------------------------------------------------------------------------------- -->

              <div>
                <v-row>
                  <v-col cols="6">
                    <v-row justify="center">
                      <v-col cols="8" align="center" pt-0 ma-0>
                        <p class="font-weight-bold" mb-0 pa-0>GEAR</p>
                      </v-col>
                    </v-row>

                    <div>
                      <v-row align="center" justify="center">
                        <v-col cols="4" align="center">
                          <v-header align="center">MCS</v-header>
                        </v-col>
                        <v-col cols="4">
                          <v-text-field
                            v-model="postdata.Column5"
                            type="number"
                          ></v-text-field>
                        </v-col>
                      </v-row>
                      <v-row justify="center">
                        <v-col cols="4">
                          <p class="font-weight-bold" align="center">
                            Tensile Side
                          </p>
                        </v-col>
                        <v-col cols="4">
                          <p class="font-weight-bold" align="center">
                            Compression Side
                          </p>
                        </v-col>
                      </v-row>

                      <div>
                        <v-row align="center" justify="center">
                          <v-col cols="4">
                            <v-text-field
                              label="Rib"
                              solo
                              dense
                              v-model="postdata.Column8"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              label="Rib"
                              solo
                              dense
                              v-model="postdata.Column9"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>

                        <v-row align="center" justify="center">
                          <v-col cols="4">
                            <v-text-field
                              label="Root"
                              solo
                              dense
                              v-model="postdata.Column7"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              label="Root"
                              solo
                              dense
                              v-model="postdata.Column10"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>

                        <v-row align="center" justify="center">
                          <v-col cols="4" class="py-1" py-1>
                            <v-text-field
                              label="Web"
                              solo
                              dense
                              v-model="postdata.Column6"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4" class="py-1" py-1>
                            <v-text-field
                              label="Web"
                              solo
                              dense
                              v-model="postdata.Column11"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <!-- <input
                            hidden="true"
                            type="file"
                            ref="gearF1"
                            @change="filechange1"
                          />

                          <input
                            hidden="true"
                            type="file"
                            ref="gearF2"
                            @change="filechange2"
                          />
                          <input
                            hidden="true"
                            type="file"
                            ref="gearP1"
                            @change="filechange3"
                          />
                          <input
                            hidden="true"
                            type="file"
                            ref="gearP2"
                            @change="filechange4"
                          /> -->
                        </v-row>

                        <!-- <v-row align="center" justify="center">
                          <v-col cols="6">
                            <v-btn @click="gf1()">Gear Feasible1</v-btn>
                          </v-col>
                          <v-col cols="6" align="left" justify="left">
                            <p class="mb-0">{{ postdata.namegf1 }}</p>
                          </v-col>
                        </v-row>

                        <v-row align="center" justify="center">
                          <v-col cols="6">
                            <v-btn @click="gf2()">Gear Feasible2</v-btn>
                          </v-col>
                          <v-col cols="6" align="left" justify="left">
                            <p class="mb-0">{{ postdata.namegf2 }}</p>
                          </v-col>
                        </v-row>

                        <v-row align="center" justify="center">
                          <v-col cols="6">
                            <v-btn @click="gp1()">Gear Physical1</v-btn>
                          </v-col>
                          <v-col cols="6" align="left" justify="left">
                            <p class="mb-0">{{ postdata.namegp1 }}</p>
                          </v-col>
                        </v-row>

                        <v-row align="center" justify="center">
                          <v-col cols="6">
                            <v-btn @click="gp2()">Gear Physical2</v-btn>
                          </v-col>
                          <v-col cols="6" align="left" justify="left">
                            <p class="mb-0">{{ postdata.namegp2 }}</p>
                          </v-col>
                        </v-row> -->
                      </div>
                    </div>
                  </v-col>

                  <!-- *************************************** -->

                  <v-col cols="6">
                    <div>
                      <v-row justify="center">
                        <v-col cols="8" align="center">
                          <p class="font-weight-bold" mb-0 pa-0>PINION</p>
                        </v-col>
                      </v-row>
                    </div>

                    <div>
                      <div>
                        <v-row align="center" justify="center">
                          <v-col cols="4" align="center">
                            <v-header align="center">MCS</v-header>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              v-model="postdata.Column12"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>
                        <v-row justify="center">
                          <v-col cols="4">
                            <p class="font-weight-bold" align="center">
                              Tensile Side
                            </p>
                          </v-col>
                          <v-col cols="4">
                            <p class="font-weight-bold" align="center">
                              Compression Side
                            </p>
                          </v-col>
                        </v-row>
                      </div>

                      <div>
                        <v-row align="left" justify="center">
                          <v-col cols="4">
                            <v-text-field
                              label="Rib"
                              solo
                              dense
                              v-model="postdata.Column13"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              label="Rib"
                              solo
                              dense
                              v-model="postdata.Column16"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>

                        <v-row align="left" justify="center">
                          <v-col cols="4">
                            <v-text-field
                              label="Root"
                              solo
                              dense
                              v-model="postdata.Column14"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              label="Root"
                              solo
                              dense
                              v-model="postdata.Column17"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>

                        <v-row align="left" justify="center">
                          <v-col cols="4" py-1 class="py-1">
                            <v-text-field
                              label="Web"
                              solo
                              dense
                              v-model="postdata.Column15"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4" class="py-1" py-1>
                            <v-text-field
                              label="Web"
                              solo
                              dense
                              v-model="postdata.Column18"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <!-- <input
                            hidden="true"
                            type="file"
                            ref="pinionF1"
                            @change="filechange5"
                          />

                          <input
                            hidden="true"
                            type="file"
                            ref="pinionF2"
                            @change="filechange6"
                          />
                          <input
                            hidden="true"
                            type="file"
                            ref="pinionP1"
                            @change="filechange7"
                          />
                          <input
                            hidden="true"
                            type="file"
                            ref="pinionP2"
                            @change="filechange8"
                          /> -->
                        </v-row>

                        <!-- <v-row align="center" justify="center">
                          <v-col cols="6">
                            <v-btn @click="pf1()">Pinion Feasible1</v-btn>
                          </v-col>
                          <v-col cols="6" align="left" justify="left">
                            <p class="mb-0">{{ postdata.namepf1 }}</p>
                          </v-col>
                        </v-row>

                        <v-row align="center" justify="center">
                          <v-col cols="6">
                            <v-btn @click="pf2()">Pinion Feasible2</v-btn>
                          </v-col>
                          <v-col cols="6" align="left" justify="left">
                            <p class="mb-0">{{ postdata.namepf2 }}</p>
                          </v-col>
                        </v-row>

                        <v-row align="center" justify="center">
                          <v-col cols="6">
                            <v-btn @click="pp1()">Pinion Physical1</v-btn>
                          </v-col>
                          <v-col cols="6" align="left" justify="left">
                            <p class="mb-0">{{ postdata.namepp1 }}</p>
                          </v-col>
                        </v-row>

                        <v-row align="center" justify="center">
                          <v-col cols="6">
                            <v-btn @click="pp2()">Pinion Physical2</v-btn>
                          </v-col>
                          <v-col cols="6" align="left" justify="left">
                            <p class="mb-0">{{ postdata.namepp2 }}</p>
                          </v-col>
                        </v-row> -->
                      </div>
                    </div>
                  </v-col>
                </v-row>
              </div>
            </v-container>

            <div>
              <v-row justify="center">
                <v-col cols="3" align="center">
                  <v-text-field
                    label="Remark"
                    solo
                    dense
                    v-model="postdata.Column19"
                    type="number"
                  >
                  </v-text-field>
                </v-col>
              </v-row>
            </div>
          </v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="primary"
              text
              class="ma-2 px-2"
              @click="dialog = false"
            >
              Cancel
            </v-btn>
            <v-btn color="primary" text @click="save1()" class="ma-2 px-2">
              Save
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>

      <!-- ------------------------------------------------------------------------------------------------- -->
      <!-- ------------------------------------------------------------------------------------------------- -->

      <v-dialog v-model="dialog1" width="900">
        <v-card>
          <v-card-title class="text-h5 grey lighten-2">
            UPDATE DATA HERE
          </v-card-title>

          <v-divider></v-divider>

          <!-- ---------------------------------------------------------------------------------------------------- -->

          <v-card-text>
            <div ma-0>
              <v-row class="text-center" justify="center" align="center">
                <v-col cols="3">
                  <v-header class="font-weight-medium"> GEAR PAIR </v-header>
                </v-col>

                <v-col cols="3">
                  <v-select
                    v-model="editdata.Project"
                    :items="DTList"
                    label="Select"
                    persistent-hint
                    return-object
                    single-line
                  >
                  </v-select>
                </v-col>
              </v-row>

              <v-row
                class="text-center"
                justify="center"
                align="center"
                pa-0
                ma-0
                mt-0
              >
                <v-col cols="3" pa-0 ma-0>
                  <v-header class="font-weight-medium" pa-0 ma-0>
                    Differential Torque
                  </v-header>
                </v-col>

                <v-col cols="3" pa-0 ma-0>
                  <v-select
                    v-model="editdata.JJ01"
                    :items="items1"
                    label="Select"
                    persistent-hint
                    return-object
                    single-line
                  >
                  </v-select>
                </v-col>
              </v-row>

              <v-row class="text-center" justify="center" align="center">
                <v-col cols="3">
                  <v-header class="font-weight-medium"> Application </v-header>
                </v-col>

                <v-col cols="3">
                  <v-select
                    v-model="editdata.Column3"
                    :items="Application"
                    label="Select"
                    persistent-hint
                    return-object
                    single-line
                  >
                  </v-select>
                </v-col>
              </v-row>

              <v-row class="text-center" justify="center" align="center">
                <v-col cols="3">
                  <v-header class="font-weight-medium" pa-0> STEPS </v-header>
                </v-col>

                <v-col cols="3">
                  <v-select
                    v-model="editdata.Report"
                    :items="items"
                    label="Select"
                    persistent-hint
                    return-object
                    single-line
                  >
                  </v-select>
                </v-col>
              </v-row>
            </div>
            <br /><br />

            <v-container>
              <!-- --------------------------------------------------------------------------------------------------- -->

              <div>
                <v-row>
                  <v-col cols="6">
                    <v-row justify="center">
                      <v-col cols="8" align="center" pt-0 ma-0>
                        <p class="font-weight-bold" mb-0 pa-0>GEAR</p>
                      </v-col>
                    </v-row>

                    <div>
                      <v-row align="center" justify="center">
                        <v-col cols="4" align="center">
                          <v-header align="center">MCS</v-header>
                        </v-col>
                        <v-col cols="4">
                          <v-text-field
                            v-model="editdata.Column5"
                            type="number"
                          ></v-text-field>
                        </v-col>
                      </v-row>
                      <v-row justify="center">
                        <v-col cols="4">
                          <p class="font-weight-bold" align="center">
                            Tensile Side
                          </p>
                        </v-col>
                        <v-col cols="4">
                          <p class="font-weight-bold" align="center">
                            Compression Side
                          </p>
                        </v-col>
                      </v-row>

                      <div>
                        <v-row align="center" justify="center">
                          <v-col cols="4">
                            <v-text-field
                              label="Rib"
                              solo
                              dense
                              v-model="editdata.Column8"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              label="Rib"
                              solo
                              dense
                              v-model="editdata.Column9"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>

                        <v-row align="center" justify="center">
                          <v-col cols="4">
                            <v-text-field
                              label="Root"
                              solo
                              dense
                              v-model="editdata.Column7"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              label="Root"
                              solo
                              dense
                              v-model="editdata.Column10"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>

                        <v-row align="center" justify="center">
                          <v-col cols="4">
                            <v-text-field
                              label="Web"
                              solo
                              dense
                              v-model="editdata.Column6"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              label="Web"
                              solo
                              dense
                              v-model="editdata.Column11"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>

                        <!-- <v-row align="center">
                          <v-col cols="8" align="center">
                            <v-btn depressed color="primary" @click="save1">
                              SAVE
                            </v-btn>
                          </v-col>
                        </v-row> -->
                      </div>
                    </div>
                  </v-col>

                  <!-- *************************************** -->

                  <v-col cols="6">
                    <div>
                      <v-row justify="center">
                        <v-col cols="8" align="center">
                          <p class="font-weight-bold" mb-0 pa-0>PINION</p>
                        </v-col>
                      </v-row>
                    </div>

                    <div>
                      <div>
                        <v-row align="center" justify="center">
                          <v-col cols="4" align="center">
                            <v-header align="center">MCS</v-header>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              v-model="editdata.Column12"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>
                        <v-row justify="center">
                          <v-col cols="4">
                            <p class="font-weight-bold" align="center">
                              Tensile Side
                            </p>
                          </v-col>
                          <v-col cols="4">
                            <p class="font-weight-bold" align="center">
                              Compression Side
                            </p>
                          </v-col>
                        </v-row>
                      </div>

                      <div>
                        <v-row align="left" justify="center">
                          <v-col cols="4">
                            <v-text-field
                              label="Rib"
                              solo
                              dense
                              v-model="editdata.Column13"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              label="Rib"
                              solo
                              dense
                              v-model="editdata.Column16"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>

                        <v-row align="left" justify="center">
                          <v-col cols="4">
                            <v-text-field
                              label="Root"
                              solo
                              dense
                              v-model="editdata.Column14"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              label="Root"
                              solo
                              dense
                              v-model="editdata.Column17"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>

                        <v-row align="left" justify="center">
                          <v-col cols="4">
                            <v-text-field
                              label="Web"
                              solo
                              dense
                              v-model="editdata.Column15"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="4">
                            <v-text-field
                              label="Web"
                              solo
                              dense
                              v-model="editdata.Column18"
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>
                      </div>
                    </div>
                  </v-col>
                </v-row>
              </div>
            </v-container>

            <div>
              <v-row justify="center">
                <v-col cols="3" align="center">
                  <v-text-field
                    label="Remark"
                    solo
                    dense
                    v-model="editdata.Column19"
                    type="number"
                  >
                  </v-text-field>
                </v-col>
              </v-row>
            </div>
          </v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="primary"
              text
              class="ma-2 px-2"
              @click="dialog1 = false"
            >
              Cancel
            </v-btn>
            <v-btn color="primary" text @click="update()" class="ma-2 px-2">
              Update
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>
    

    <v-data-table
      v-model="selected1"
      :headers="headers"
      :items="SAM"
      :single-select="singleSelect1"
      item-key="_id"
      show-select
      class="elevation-1"
      id="ttable1"
    >

    <template v-for="(col1, i) in filters1"  v-slot:[`header.${i}`]="{ header }" >
        <div style="display: inline-block; padding: 0px 0;" :key="col1"> {{header.text}}</div>
        <div style="float: right; margin-top: 0px" :key="col1" >
          <v-menu :close-on-content-click="false" :nudge-width="200" offset-y transition="slide-y-transition" left fixed style="position: absolute; right: 8px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="indigo" icon v-bind="attrs" v-on="on">
                <v-icon small 
                  :color="activeFilters1[header.value].length >0 ? 'red' : 'default'">
                  mdi-filter-variant
                </v-icon>
              </v-btn>
            </template >
<v-card>

  <v-combobox
  v-if="check(header.value)==='project'"
      v-model="SortedGearPair"
      :items="GearPair"
      label="Select GearPair"
      class="pt-6 pb-2 ml-3"
     background-color="white"
     v-bind="attrs"
    v-on="listeners"
    
    
      multiple
    >
    <template v-slot:selection="">
     
    </template>
  </v-combobox>
    
                  <v-combobox
                v-if="check(header.value)==='jj01'"
                    v-model="SortedDT"
                    :items="items1"
                    label="Select Differential Torque"
                    class="pt-6 pb-2 ml-3"
                    
                    multiple
                  ></v-combobox>
    
                  <v-combobox
                v-if="check(header.value)==='column3'"
                    v-model="SortedApplication"
                    :items="Application"
                    label="Select Application"
                    class="pt-6 pb-2 ml-3"
                   
                    multiple
                  ></v-combobox>
    
                  <v-combobox
                v-if="check(header.value)==='report'"
                    v-model="SortedSteps"
                    :items="items"
                    label="Select Steps"
                    class="pt-6 pb-2 ml-3"
                   
                    multiple
                  ></v-combobox>
</v-card>

              <v-card v-if="check(header.value)==='mcs1'" >
               
              <v-text-field
                v-model="greatermcs1"
                type="number"
                label="Greater than"
              ></v-text-field>
           
              <v-text-field
                v-model="lessmcs1"
                type="number"
                label="Less than"
              ></v-text-field>
          
              </v-card>

              <v-card v-if="check(header.value)==='rib1'" >
               
               <v-text-field
                 v-model="greaterrib1"
                 type="number"
                 label="Greater than"
               ></v-text-field>
            
               <v-text-field
                 v-model="lessrib1"
                 type="number"
                 label="Less than"
               ></v-text-field>
           
               </v-card>

               <v-card v-if="check(header.value)==='root1'" >
               
               <v-text-field
                 v-model="greaterroot1"
                 type="number"
                 label="Greater than"
               ></v-text-field>
            
               <v-text-field
                 v-model="lessroot1"
                 type="number"
                 label="Less than"
               ></v-text-field>
           
               </v-card>

               <v-card v-if="check(header.value)==='web1'" >
               
               <v-text-field
                 v-model="greaterweb1"
                 type="number"
                 label="Greater than"
               ></v-text-field>
            
               <v-text-field
                 v-model="lessweb1"
                 type="number"
                 label="Less than"
               ></v-text-field>
           
               </v-card>

               <v-card v-if="check(header.value)==='rib2'" >
                
                <v-text-field
                  v-model="greaterrib2"
                  type="number"
                  label="Greater than"
                ></v-text-field>
             
                <v-text-field
                  v-model="lessrib2"
                  type="number"
                  label="Less than"
                ></v-text-field>
            
                </v-card>
 
                <v-card v-if="check(header.value)==='root2'" >
                
                <v-text-field
                  v-model="greaterroot2"
                  type="number"
                  label="Greater than"
                ></v-text-field>
             
                <v-text-field
                  v-model="lessroot2"
                  type="number"
                  label="Less than"
                ></v-text-field>
            
                </v-card>
 
                <v-card v-if="check(header.value)==='web2'" >
                
                <v-text-field
                  v-model="greaterweb2"
                  type="number"
                  label="Greater than"
                ></v-text-field>
             
                <v-text-field
                  v-model="lessweb2"
                  type="number"
                  label="Less than"
                ></v-text-field>
            
                </v-card>



                <v-card v-if="check(header.value)==='mcs2'" >
               
               <v-text-field
                 v-model="greatermcs2"
                 type="number"
                 label="Greater than"
               ></v-text-field>
            
               <v-text-field
                 v-model="lessmcs2"
                 type="number"
                 label="Less than"
               ></v-text-field>
           
               </v-card>
               <v-card v-if="check(header.value)==='rib3'" >
                
                <v-text-field
                  v-model="greaterrib3"
                  type="number"
                  label="Greater than"
                ></v-text-field>
             
                <v-text-field
                  v-model="lessrib3"
                  type="number"
                  label="Less than"
                ></v-text-field>
            
                </v-card>
 
                <v-card v-if="check(header.value)==='root3'" >
                
                <v-text-field
                  v-model="greaterroot3"
                  type="number"
                  label="Greater than"
                ></v-text-field>
             
                <v-text-field
                  v-model="lessroot3"
                  type="number"
                  label="Less than"
                ></v-text-field>
            
                </v-card>
 
                <v-card v-if="check(header.value)==='web3'" >
                
                <v-text-field
                  v-model="greaterweb3"
                  type="number"
                  label="Greater than"
                ></v-text-field>
             
                <v-text-field
                  v-model="lessweb3"
                  type="number"
                  label="Less than"
                ></v-text-field>
            
                </v-card>
 
                <v-card v-if="check(header.value)==='rib4'" >
                 
                 <v-text-field
                   v-model="greaterrib4"
                   type="number"
                   label="Greater than"
                 ></v-text-field>
              
                 <v-text-field
                   v-model="lessrib4"
                   type="number"
                   label="Less than"
                 ></v-text-field>
             
                 </v-card>
  
                 <v-card v-if="check(header.value)==='root4'" >
                 
                 <v-text-field
                   v-model="greaterroot4"
                   type="number"
                   label="Greater than"
                 ></v-text-field>
              
                 <v-text-field
                   v-model="lessroot4"
                   type="number"
                   label="Less than"
                 ></v-text-field>
             
                 </v-card>
  
                 <v-card v-if="check(header.value)==='web4'" >
                 
                 <v-text-field
                   v-model="greaterweb4"
                   type="number"
                   label="Greater than"
                 ></v-text-field>
              
                 <v-text-field
                   v-model="lessweb4"
                   type="number"
                   label="Less than"
                 ></v-text-field>
             
                 </v-card>

                 <v-card v-if="check(header.value)==='remark'" >
                 
                 <v-text-field
                   v-model="Gremark"
                   type="number"
                   label="Greater than"
                 ></v-text-field>
              
                 <v-text-field
                   v-model="Lremark"
                   type="number"
                   label="Less than"
                 ></v-text-field>
             
                 </v-card>


<!--             <v-list flat dense class="pa-0" v-if="counter(header.value)==='sambhaji'">
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
            </v-list> -->
          </v-menu>
        </div>
      </template>
      


    </v-data-table>
  </v-app>
</template>

<style>

/* .v-list--dense .v-list-item, .v-list-item--dense {
  min-height: 20px !important;
  height: 2rem;
}

.v-application--is-ltr .v-list-item__action:first-child, .v-application--is-ltr .v-list-item__icon:first-child {
  margin-right: .5rem !important;
}

.v-list-item--link {
  transition: background-color .3s cubic-bezier(.25,.8,.5,1);
}

.v-list-item--link:hover {
  background-color: rgba(0,0,0, .13);
} */

#b1 {
  margin-left: 44%;
  margin-top: 30px;
  margin-bottom: 30px;
}

.row + .row {
  margin-top: 1px;
}

.row {
  margin: -16px;
}

.row {
  margin: -16px;
}
html {
  overflow-y: auto;
}
</style>

<script>
import axios from "axios";

import * as firebase from "firebase/app";

import {
  getStorage,
  ref,
  uploadBytesResumable,
  getDownloadURL,
} from "firebase/storage";

const firebaseConfig = {
  apiKey: "AIzaSyBsAdm3QQTHlmwMihKSaXcEjcx-cwOeX8c",
  authDomain: "project-360e7.firebaseapp.com",
  projectId: "project-360e7",
  storageBucket: "project-360e7.appspot.com",
  messagingSenderId: "921356772970",
  appId: "1:921356772970:web:362f876a5d94e3ae280c13",
};

// Initialize Firebase
firebase.initializeApp(firebaseConfig);
//script
export default {
  data() {
    return {
      select: { state: "" },
      items: [
        { text: "GTPR", value: "GTPR" },
        { text: "PCD", value: "PCD" },
        { text: "PTGR", value: "PTGR" },
      ],
      items1: [
        { text: "1000", value: 1000 },
        { text: "2000", value: 2000 },
        { text: "3000", value: 3000 },
        { text: "4000", value: 4000 },
        { text: "5000", value: 5000 },
        { text: "6000", value: 6000 },
        { text: "4500", value: 4500 },
        { text: "5500", value: 5500 },
      ],

      DTList: ["JJ01-A1B1", "JJ01-A1B2", "JJ01-A1B3", "JJ01-A1B4"],

      Application: [
        { text: "2Pinion", value: "2Pinion" },
        { text: "4Pinion", value: "4Pinion" },
      ],

      GearPair: [
        // { text: "All", value: null },

        { text: "JJ01-A1B1", value: "JJ01-A1B1" },
        { text: "JJ01-A1B2", value: "JJ01-A1B2" },
        { text: "JJ01-A1B3", value: "JJ01-A1B3" },
        { text: "JJ01-A1B4", value: "JJ01-A1B4" },
      ],

      SortList: [
        { text: "Gear MCS", value: "mcs1" },
        { text: "Pinion MCS", value: "mcs2" },
        { text: "Gear Tensile Rib", value: "rib1" },
        { text: "Gear Tensile Root", value: "root1" },
        { text: "Gear Tensile Web", value: "web1" },
        { text: "Pinion Compression Rib", value: "rib2" },
        { text: "Pinion Compression Root", value: "root2" },
        { text: "Pinion Compression Web", value: "web2" },
      ],

      DTFilterValue: null,
      SortedValue: [],
      SortedValue1: [],
      SortedGearPair: [],
      SortedDT: [],
      SortedApplication: [],
      SortedSteps: [],

      less: "",
      greater: "",

      greatermcs1: "",
      greatermcs2: "",
      greaterrib1: "",
      greaterroot1: "",
      greaterweb1: "",
      greaterrib2: "",
      greaterroot2: "",
      greaterweb2: "",
      greaterrib3: "",
      greaterroot3: "",
      greaterweb3: "",
      greaterrib4: "",
      greaterroot4: "",
      greaterweb4: "",

      lessmcs1: "",
      lessmcs2: "",
      lessrib1: "",
      lessroot1: "",
      lessweb1: "",
      lessrib2: "",
      lessroot2: "",
      lessweb2: "",
      lessrib3: "",
      lessroot3: "",
      lessweb3: "",
      lessrib4: "",
      lessroot4: "",
      lessweb4: "",
      Gremark:"",
      Lremark:"",

      singleSelect1: true,
      selected1: [],
      disableb: true,
      dialog: false,
      dialog1: false,
      filters1:{'Project': [], 'JJ01': [], 'Column3': [],'Report':[],'Column5':[],'Column6':[],'Column7':[],'Column8':[],'Column9':[],'Column10':[],'Column11':[],'Column12':[],'Column13':[],'Column14':[],'Column15':[],'Column16':[],'Column17':[],'Column18':[],'Column19':[]},
      activeFilters1: {},
      
      key:1,

      path1: "/Dashboard/ ",
      path2: "/Dashboard/",
      checkpointer1: false,

      SAM: [],

      selectedfile: null,

      Sgf1: false,
      Sgf2: false,
      Sgp1: false,
      Sgp2: false,

      Spf1: false,
      Spf2: false,
      Spp1: false,
      Spp2: false,

      namegf1: null,

      projectclick: false,
      dtselected: false,
      selectedStep: "",
      allselect: false,
      duplicate: "sam",

      postdata: {
        Project: "",
        JJ01: "",
        Column3: "",
        Report: "",
        Column5: "",
        Column6: "",
        Column7: "",
        Column8: "",
        Column9: "",
        Column10: "",
        Column11: "",
        Column12: "",
        Column13: "",
        Column14: "",
        Column15: "",
        Column16: "",
        Column17: "",
        Column18: "",
        Column19: "",
        // GF1: "",
        // GF2: "",
        // GP1: "",
        // GP2: "",
        // PF1: "",
        // PF2: "",
        // PP1: "",
        // PP2: "",
        // namegf1: "no file selected",
        // namegf2: "no file selected",
        // namegp1: "no file selected",
        // namegp2: "no file selected",

        // namepf1: "no file selected",
        // namepf2: "no file selected",
        // namepp1: "no file selected",
        // namepp2: "no file selected",
      },

      editdata: {
        Project: "",
        JJ01: "",
        Column3: "",
        Report: "",
        Column5: "",
        Column6: "",
        Column7: "",
        Column8: "",
        Column9: "",
        Column10: "",
        Column11: "",
        Column12: "",
        Column13: "",
        Column14: "",
        Column15: "",
        Column16: "",
        Column17: "",
        Column18: "",
        Column19: "",
      },
    };
  },

  watch:{
    SortedGearPair (val){
      this.activeFilters1['Project']=val;
    },
    SortedApplication(val){
      this.activeFilters1['Column3']=val
    },
    SortedDT(val){
      this.activeFilters1['JJ01']=val
    },
    SortedSteps(val){
      this.activeFilters1['Report']=val
    }

  },
  computed: {
    headers() {
      return [
        {
          text: "Gear Pair",
          align: "left",
          sortable: false,
          value: "Project",
          // filter: this.DTFilter,
          filter: (value) => {
            // console.log("sortedgearpair : ",this.SortedGearPair)
            console.log("activefilters : ",this.activeFilters1)
            // console.log("filters : ",this.filters1)
            // var valObj = this.SortedGearPair.filter(function (elem) {
            //   if (elem.value == "JJ01-A1B1") {
            //     return elem.value;
            //   }
            // });
            // console.log("valobjproject : ",valObj)

            let SortedGearPair1=[];
            if(this.SortedGearPair){

              var valObj = this.SortedGearPair.filter(function (elem) {
              // console.log("element : ",elem.value)
              SortedGearPair1.push(elem.value)
                return elem.value;
              
            });
            }
            console.log("valobjproject : ",valObj)

            // let item;
            // for( item in this.SortedGearPair){
            //   console.log("item : ",item)
            //   SortedGearPair1.push(item.value)
            // }
            // console.log("SortedGearpair1 : ",SortedGearPair1)
            if (!SortedGearPair1.length) {
              return true;
            } else {
              console.log("I am in else");
              let val = SortedGearPair1.includes(value);

              if (val) {
                return value;
              }
            }
          },
          // filter: value => {
          //   return this.activeFilters.Project.includes(value);
          // },
        },
        {
          text: "Differential \nTorque",
          value: "JJ01",
          // filter: this.DTFilter,
          filter: (value) => {
            let SortedDT1=[];
            if(this.SortedDT){

              var valObj = this.SortedDT.filter(function (elem) {
          
              SortedDT1.push(elem.value)
                return elem.value;
              
            });
            }
            console.log("valobjproject : ",valObj)
            if (!SortedDT1.length) {
              return true;
            } else {
              let val = SortedDT1.includes(value);

              if (val) {
                return value;
              }
            }
          },
        },
        {
          text: "Application",
          value: "Column3",
          filter: (value) => {
            let SortedApplication1=[];
            if(this.SortedApplication){

              var valObj = this.SortedApplication.filter(function (elem) {
          
              SortedApplication1.push(elem.value)
                return elem.value;
              
            });
            }
            console.log("valobjproject : ",valObj)
            if (!SortedApplication1.length) {
              return true;
            } else {
              let val = SortedApplication1.includes(value);

              if (val) {
                return value;
              }
            }
          },
        },
        {
          text: "Step",
          value: "Report",
          filter: (value) => {

            let SortedSteps1=[];
            if(this.SortedSteps){

              var valObj = this.SortedSteps.filter(function (elem) {
          
              SortedSteps1.push(elem.value)
                return elem.value;
              
            });
            }
            console.log("valobjproject : ",valObj)
            if (!SortedSteps1.length) {
              return true;
            } else {
              let val = SortedSteps1.includes(value);

              if (val) {
                return value;
              }
            }
          },
        },
        {
          text: "MCS",
          value: "Column5",
          filter: (value) => {
            // console.log("mcs1 value is :", value);
            // let samarray=[]
            // console.log("selected array : ", this.SortedValue);
            // var valObj = this.SortedValue.filter(function (elem) {
            //   if (elem.value == "mcs1") {
            //     // samarray.push(elem.value)
            //     return elem.value;
            //   }
            // });
            // // console.log("valobjmcs1 : ",valObj)
            // // console.log("samarray : ",samarray)
            // if (valObj.length) {
            //   this.SortGmcs1 = this.greater;
            //   this.SortLmcs1 = this.less;
            // } else {
            //   this.SortGmcs1 = "";
            //   this.SortLmcs1 = "";
            // }
            // console.log("Gmcs : ", this.SortGmcs1);
            if (!this.lessmcs1 && !this.greatermcs1) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessmcs1 && !this.greatermcs1) {
              let S = value <= parseInt(this.lessmcs1);
              return S;
            } else if (!this.lessmcs1 && this.greatermcs1) {
              let S = value >= parseInt(this.greatermcs1);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessmcs1) &&
                value >= parseInt(this.greatermcs1);
              return S;
            }
          },
        },
        {
          text: "Rib (MBS)",
          value: "Column6",
          filter: (value) => {
            // console.log("rib1 value is :", value);
            // var valObj = this.SortedValue.filter(function (elem) {
            //   if (elem.value == "rib1") return elem.value;
            // });

            // if (valObj.length) {
            //   this.SortGrib1 = this.greater;
            //   this.SortLrib1 = this.less;
            //   // console.log("Grib : ", this.SortGrib1);
            // } else {
            //   this.SortGrib1 = "";
            //   this.SortLrib1 = "";
            // }
            // console.log("Grib : ", this.SortGrib1)
            if (!this.lessrib1 && !this.greaterrib1) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessrib1 && !this.greaterrib1) {
              let S = value <= parseInt(this.lessrib1);
              return S;
            } else if (!this.lessrib1 && this.greaterrib1) {
              let S = value >= parseInt(this.greaterrib1);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessrib1) &&
                value >= parseInt(this.greaterrib1);
              return S;
            }
          },
        },
        {
          text: "Root (MBS)",
          value: "Column7",
          filter: (value) => {
            // console.log("root1 value is :", value);
            // var valObj = this.SortedValue.filter(function (elem) {
            //   if (elem.value == "root1") return elem.value;
            // });

            // if (valObj.length) {
            //   this.SortGroot1 = this.greater;
            //   this.SortLroot1 = this.less;
            //   // console.log("Groot : ", this.SortGroot1);
            // } else {
            //   this.SortGroot1 = "";
            //   this.SortLroot1 = "";
            // }
            // console.log("Groot : ", this.SortGroot1)
            if (!this.lessroot1 && !this.greaterroot1) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessroot1 && !this.greaterroot1) {
              let S = value <= parseInt(this.lessroot1);
              return S;
            } else if (!this.lessroot1 && this.greaterroot1) {
              let S = value >= parseInt(this.greaterroot1);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessroot1) &&
                value >= parseInt(this.greaterroot1);
              return S;
            }
          },
        },
        {
          text: "Web (MBS)",
          value: "Column8",
          filter: (value) => {
            // var valObj = this.SortedValue.filter(function (elem) {
            //   if (elem.value == "web1") return elem.value;
            // });

            // if (valObj.length) {
            //   this.SortGweb1 = this.greater;
            //   this.SortLweb1 = this.less;
            // } else {
            //   this.SortGweb1 = "";
            //   this.SortLweb1 = "";
            // }
            if (!this.lessweb1 && !this.greaterweb1) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessweb1 && !this.greaterweb1) {
              let S = value <= parseInt(this.lessweb1);
              return S;
            } else if (!this.lessweb1 && this.greaterweb1) {
              let S = value >= parseInt(this.greaterweb1);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessweb1) &&
                value >= parseInt(this.greaterweb1);
              return S;
            }
          },
        },
        {
          text: "Rib (MBS)",
          value: "Column9",
          filter: (value) => {
            // var valObj = this.SortedValue.filter(function (elem) {
            //   if (elem.value == "rib2") return elem.value;
            // });

            // if (valObj.length) {
            //   this.SortGrib2 = this.greater;
            //   this.SortLrib2 = this.less;
            // } else {
            //   this.SortGrib2 = "";
            //   this.SortLrib2 = "";
            // }
            if (!this.lessrib2 && !this.greaterrib2) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessrib2 && !this.greaterrib2) {
              let S = value <= parseInt(this.lessrib2);
              return S;
            } else if (!this.lessrib2 && this.greaterrib2) {
              let S = value >= parseInt(this.greaterrib2);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessrib2) &&
                value >= parseInt(this.greaterrib2);
              return S;
            }
          },
        },
        {
          text: "Root (MBS)",
          value: "Column10",
          filter: (value) => {
            // var valObj = this.SortedValue.filter(function (elem) {
            //   if (elem.value == "root2") return elem.value;
            // });

            // if (valObj.length) {
            //   this.SortGroot2 = this.greater;
            //   this.SortLroot2 = this.less;
            // } else {
            //   this.SortGroot2 = "";
            //   this.SortLroot2 = "";
            // }
            if (!this.lessroot2 && !this.greaterroot2) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessroot2 && !this.greaterroot2) {
              let S = value <= parseInt(this.lessroot2);
              return S;
            } else if (!this.lessroot2 && this.greaterroot2) {
              let S = value >= parseInt(this.greaterroot2);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessroot2) &&
                value >= parseInt(this.greaterroot2);
              return S;
            }
          },
        },
        {
          text: "Web (MBS)",
          value: "Column11",
          filter: (value) => {
          
            if (!this.lessweb2 && !this.greaterweb2) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessweb2 && !this.greaterweb2) {
              let S = value <= parseInt(this.lessweb2);
              return S;
            } else if (!this.lessweb2 && this.greaterweb2) {
              let S = value >= parseInt(this.greaterweb2);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessweb2) &&
                value >= parseInt(this.greaterweb2);
              return S;
            }
          },
        },
        {
          text: "MCS",
          value: "Column12",
          filter: (value) => {
            // var valObj = this.SortedValue.filter(function (elem) {
            //   if (elem.value == "mcs2") return elem.value;
            // });

            // if (valObj.length) {
            //   this.SortGmcs2 = this.greater;
            //   this.SortLmcs2 = this.less;
            // } else {
            //   this.SortGmcs2 = "";
            //   this.SortLmcs2 = "";
            // }
            if (!this.lessmcs2 && !this.greatermcs2) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessmcs2 && !this.greatermcs2) {
              let S = value <= parseInt(this.lessmcs2);
              return S;
            } else if (!this.lessmcs2 && this.greatermcs2) {
              let S = value >= parseInt(this.greatermcs2);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessmcs2) &&
                value >= parseInt(this.greatermcs2);
              return S;
            }
          },
        },
        { text: "Rib (MBS)", value: "Column13" ,
          filter: (value) => {
          
            if (!this.lessrib3 && !this.greaterrib3) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessrib3 && !this.greaterrib3) {
              let S = value <= parseInt(this.lessrib3);
              return S;
            } else if (!this.lessrib3 && this.greaterrib3) {
              let S = value >= parseInt(this.greaterrib3);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessrib3) &&
                value >= parseInt(this.greaterrib3);
              return S;
            }
          },},
        { text: "Root (MBS)", value: "Column14" 
        ,
          filter: (value) => {
          
            if (!this.lessroot3 && !this.greaterroot3) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessroot3 && !this.greaterroot3) {
              let S = value <= parseInt(this.lessroot3);
              return S;
            } else if (!this.lessroot3 && this.greaterroot3) {
              let S = value >= parseInt(this.greaterroot3);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessroot3) &&
                value >= parseInt(this.greaterroot3);
              return S;
            }
          },
      },
        { text: "Web (MBS)", value: "Column15"  ,
          filter: (value) => {
          
            if (!this.lessweb3 && !this.greaterweb3) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessweb3 && !this.greaterweb3) {
              let S = value <= parseInt(this.lessweb3);
              return S;
            } else if (!this.lessweb3 && this.greaterweb3) {
              let S = value >= parseInt(this.greaterweb3);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessweb3) &&
                value >= parseInt(this.greaterweb3);
              return S;
            }
          }, },
        { text: "Rib (MBS)", value: "Column16"  ,
          filter: (value) => {
          
            if (!this.lessrib4 && !this.greaterrib4) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessrib4 && !this.greaterrib4) {
              let S = value <= parseInt(this.lessrib4);
              return S;
            } else if (!this.lessrib4 && this.greaterrib4) {
              let S = value >= parseInt(this.greaterrib4);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessrib4) &&
                value >= parseInt(this.greaterrib4);
              return S;
            }
          },},
        { text: "Root (MBS)", value: "Column17"  ,
          filter: (value) => {
          
            if (!this.lessroot4 && !this.greaterroot4) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessroot4 && !this.greaterroot4) {
              let S = value <= parseInt(this.lessroot4);
              return S;
            } else if (!this.lessroot4 && this.greaterroot4) {
              let S = value >= parseInt(this.greaterroot4);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessroot4) &&
                value >= parseInt(this.greaterroot4);
              return S;
            }
          }, },
        { text: "Web (MBS)", value: "Column18" 
        ,
          filter: (value) => {
          
            if (!this.lessweb4 && !this.greaterweb4) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.lessweb4 && !this.greaterweb4) {
              let S = value <= parseInt(this.lessweb4);
              return S;
            } else if (!this.lessweb4 && this.greaterweb4) {
              let S = value >= parseInt(this.greaterweb4);
              return S;
            } else {
              let S =
                value <= parseInt(this.lessweb4) &&
                value >= parseInt(this.greaterweb4);
              return S;
            }
          },
      },
        { text: "Remarks", value: "Column19"  ,
          filter: (value) => {
          
            if (!this.Lremark && !this.Gremark) return true;
            // if(this.sam) return value > parseInt(this.sam)
            if (this.Lremark && !this.Gremark) {
              let S = value <= parseInt(this.Lremark);
              return S;
            } else if (!this.Lremark && this.Gremark) {
              let S = value >= parseInt(this.Gremark);
              return S;
            } else {
              let S =
                value <= parseInt(this.Lremark) &&
                value >= parseInt(this.Gremark);
              return S;
            }
          },},
      ];
    },
  },
  mounted() {
    this.getapicall();
  },
  created() {
    this.initialize()
  },
  methods: {

initialize(){
  let col1
  for (col1 in this.filters1) {
        this.filters1[col1] = this.SAM.map((d1) => { return d1[col1] }).filter(
          (value1, index1, self1) => { return self1.indexOf(value1) === index1 }
        );
         console.log("filters1 for loop : ",this.filters1[col1])
      }
      this.activeFilters1 = Object.assign({}, this.filters1)
      console.log("ActiveFilters1 : ",this.activeFilters1)
},

check(t){
     // this.count=this.count+1
    //  console.log("counter : ",t)
     if(t==='Project'){

       return 'project'
     }
     else if(t==='JJ01'){
      return 'jj01'
     }
     else if(t==='Column3'){
      return 'column3'
     }
     else if(t==='Report'){
      return 'report'
     }
     else if(t==='Column5'){
      return 'mcs1'

     }
     else if(t==='Column6'){
      return 'rib1'
     }
     else if(t==='Column7'){
      return 'root1'
     }
     else if(t==='Column8'){
      return 'web1'
     }
     else if(t==='Column9'){
      return 'rib2'
     }
     else if(t==='Column10'){
      return 'root2'
     }
     else if(t==='Column11'){
      return 'web2'
     }
     else if(t==='Column12'){
      return 'mcs2'

     }
     else if(t==='Column13'){
      return 'rib3'
     }
     else if(t==='Column14'){
      return 'root3'
     }
     else if(t==='Column15'){
      return 'web3'
     }
     else if(t==='Column16'){
      return 'rib4'
     }
     else if(t==='Column17'){
      return 'root4'
     }
     else if(t==='Column18'){
      return 'web4'
     }
     else if(t==='Column19'){
      return 'remark'
     }
          else{
       return 'samG'
     }
    
   },

    setkey(){
      this.key=this.key+1
      let Key="sam"+this.key
      return Key
    },
    SortField() {
      // this.less = "";
      // this.greater = "";
      // console.log("selected : ", this.SortedValue);
      // let p=this.SortedValue.find("mcs7")
      // let val = this.SortedValue;
      // var valObj = this.SortedValue.filter(function(elem){
      //   console.log("ele : ",elem)
      //     if(elem.value == "mcs1") return elem.value;
      // });
      // console.log("mcs find : ",valObj)
      // console.log("sorted1 : ",this.SortedValue1)
      // if (this.SortedValue == "mcs1") {
      //   console.log("mcs1 L : ", this.SortLmcs1);
      // this.SortGmcs1 = this.greater;
      // this.SortLmcs1 = this.less;
      // } else if (this.SortedValue == "rib1") {
      // this.SortGrib1 = this.greater;
      // this.SortLrib1 = this.less;
      // } else if (this.SortedValue == "root1") {
      // this.SortGroot1 = this.greater;
      // this.SortLroot1 = this.less;
      // } else if (this.SortedValue == "web1") {
      // this.SortGweb1 = this.greater;
      // this.SortLweb1 = this.less;
      // } else if (this.SortedValue == "rib2") {
      // this.SortGrib2 = this.greater;
      // this.SortLrib2 = this.less;
      // } else if (this.SortedValue == "root2") {
      // this.SortGroot2 = this.greater;
      // this.SortLroot2 = this.less;
      // } else if (this.SortedValue == "web2") {
      // this.SortGweb2 = this.greater;
      // this.SortLweb2 = this.less;
      // } else if (this.SortedValue == "mcs2") {
      // this.SortGmcs2 = this.greater;
      // this.SortLmcs2 = this.less;
      // } else {
      //   console.log("not selected");
      // }
    },

    Projectselected() {
      // this.projectclick = true;
    },
    DTselected() {
      // console.log("DT : ", this.postdata.JJ01);
      // if (this.projectclick) {
      //   // this.getapicall();
      //   this.dtselected = true;
      //   if (this.postdata.Project != "") {
      //     if (this.postdata.JJ01 != null) {
      //       if (this.postdata.Column3 != "") {
      //         // this.allselect=true;
      //         this.getapicall1();
      //       }
      //     }
      //   }
      // } else {
      //   alert("Select Project first...");
      //   this.postdata.JJ01 = null;
      // }
    },

    AppSelect() {
      // if (this.dtselected) {
      //   this.getapicall1();
      // } else {
      //   alert("Select Differential Torque first...");
      //   this.postdata.Column3 = null;
      // }
    },

    async getapicall1() {
      await axios
        .get(
          "http://localhost:8083/api/items/" +
            this.postdata.Project +
            "/" +
            this.postdata.JJ01 +
            "/" +
            this.postdata.Column3 +
            "/" +
            this.postdata.Report
        )
        .then((resp) => {
          this.SAM = resp.data;
          console.log("this.sam : ", this.SAM);

          if (this.SAM.length == 0) {
            console.log("not duplicate pair is present");
            this.abc = "not";
          } else {
            alert("Inserted duplicate Data...");
            // this.postdata.Report = null;
            this.abc = "duplicate";
            // this.postdata.JJ01 = null;
          }
        })
        .catch((err) => {
          console.log("Error : ", err);
        });
    },

    selectpost(sp) {
      console.log("selected post : ", sp);

      if (this.postdata.Project != "") {
        if (this.postdata.JJ01 != null) {
          if (this.postdata.Column3 != "") {
            this.allselect = true;
            this.getapicall1();
          } else {
            alert("Enter Application...");
            this.postdata.Report = null;
          }
        } else {
          alert("Enter Differential Torque...");
          this.postdata.Report = null;
        }
      } else {
        alert("Enter Gear Pair...");
        this.postdata.Report = null;
      }
      this.selectedStep = sp;
    },

    save2() {
      this.getapicall1();
      console.log("duplicate is : ", this.duplicate);
      if (this.duplicate == "sam2") {
        alert("Inserting wrong data...");
      } else {
        this.gtpr.Project = this.postdata.Project;
        this.pcd.Project = this.postdata.Project;
        this.ptgr.Project = this.postdata.Project;

        this.gtpr.JJ01 = this.postdata.JJ01;
        this.pcd.JJ01 = this.postdata.JJ01;
        this.ptgr.JJ01 = this.postdata.JJ01;

        this.gtpr.Column3 = this.postdata.Column3;
        this.pcd.Column3 = this.postdata.Column3;
        this.ptgr.Column3 = this.postdata.Column3;

        console.log("GTPR : ", this.gtpr);
        console.log("PCD : ", this.pcd);
        console.log("PTGR : ", this.ptgr);

        if (this.postdata.Report == "GTPR") {
          this.gtpr = this.postdata;
          console.log("This is gtpr ");
          this.save1();
        } else if (this.postdata.Report == "PCD") {
          this.pcd = this.postdata;
          this.save1();
          // this.postdata = this.gtpr;
        } else if (this.postdata.Report == "PTGR") {
          this.ptgr = this.postdata;
          // this.postdata = this.gtpr;
          this.save1();
        } else {
          alert("Please enter STEP.......");
        }
      }
    },

    async getapicall() {
      console.log("previous postdata : ", this.postdata);

      await axios
        .get("http://localhost:8083/api/items")
        // .get("http://localhost:3000/DATA1/")
        .then((resp) => {
          this.SAM = resp.data;
          this.SAM.reverse();
          console.log("this.sam : ", this.SAM);
          console.log("selected array : ", this.selected1);
        })
        .catch((err) => {
          console.log("Error : ", err);
        });
    },

    async save1() {
      if (this.postdata.Project != "") {
        if (this.postdata.JJ01 != null) {
          if (this.postdata.Column3 != "") {
            if (this.postdata.Report != null) {
              await this.getapicall1();

              if (this.abc == "duplicate") {
                return;
              }
            } else {
              alert("select Report...");
              return;
            }
          } else {
            alert("Enter Application...");
            this.postdata.Report = null;
            return;
          }
        } else {
          alert("Enter Differential Torque...");
          this.postdata.Report = null;
          return;
        }
      } else {
        alert("Enter Project...");
        this.postdata.Project = null;
        if (this.postdata.JJ01 == null) {
          this.postdata.JJ01 = null;
        }
        return;
      }

      this.dialog = false;

      await axios
        .post("http://localhost:8083/api/items", this.postdata)
        .then((result1) => {
          console.log("Result : ", result1);
          // this.pcddata();

          this.postdata = {
            Project: "",
            JJ01: "",
            Column3: "",
            Report: "",
            Column5: "",
            Column6: "",
            Column7: "",
            Column8: "",
            Column9: "",
            Column10: "",
            Column11: "",
            Column12: "",
            Column13: "",
            Column14: "",
            Column15: "",
            Column16: "",
            Column17: "",
            Column18: "",
            Column19: "",
            // GF1: "",
            // GF2: "",
            // GP1: "",
            // GP2: "",
            // PF1: "",
            // PF2: "",
            // PP1: "",
            // PP2: "",
            // namegf1: "no file selected",
            // namegf2: "no file selected",
            // namegp1: "no file selected",
            // namegp2: "no file selected",

            // namepf1: "no file selected",
            // namepf2: "no file selected",
            // namepp1: "no file selected",
            // namepp2: "no file selected",
          };
          this.getapicall();
          console.log("data inserted : ", this.SAM);
        })
        .catch((err) => {
          console.log("Error : ", err);
        });
    },

    pcddata() {
      axios
        .post("http://localhost:3000/DATA1", this.pcd)
        .then((result2) => {
          console.log(result2);
          this.ptgrdata();
        })
        .catch((err) => {
          console.log(err);
        });
    },

    ptgrdata() {
      axios
        .post("http://localhost:3000/DATA1", this.ptgr)
        .then((result3) => {
          console.log(result3);
          this.postdata = {
            Project: "",
            JJ01: "",
            Column3: "",
            Report: "",
            Column5: "",
            Column6: "",
            Column7: "",
            Column8: "",
            Column9: "",
            Column10: "",
            Column11: "",
            Column12: "",
            Column13: "",
            Column14: "",
            Column15: "",
            Column16: "",
            Column17: "",
            Column18: "",
            Column19: "",
          };
          this.gtpr = {
            Project: "",
            JJ01: "",
            Column3: "",
            Report: "GTPR",
            Column5: "",
            Column6: "",
            Column7: "",
            Column8: "",
            Column9: "",
            Column10: "",
            Column11: "",
            Column12: "",
            Column13: "",
            Column14: "",
            Column15: "",
            Column16: "",
            Column17: "",
            Column18: "",
            Column19: "",
          };
          this.pcd = {
            Project: "",
            JJ01: "",
            Column3: "",
            Report: "PCD",
            Column5: "",
            Column6: "",
            Column7: "",
            Column8: "",
            Column9: "",
            Column10: "",
            Column11: "",
            Column12: "",
            Column13: "",
            Column14: "",
            Column15: "",
            Column16: "",
            Column17: "",
            Column18: "",
            Column19: "",
          };
          this.ptgr = {
            Project: "",
            JJ01: "",
            Column3: "",
            Report: "PTGR",
            Column5: "",
            Column6: "",
            Column7: "",
            Column8: "",
            Column9: "",
            Column10: "",
            Column11: "",
            Column12: "",
            Column13: "",
            Column14: "",
            Column15: "",
            Column16: "",
            Column17: "",
            Column18: "",
            Column19: "",
          };
          this.getapicall();
          // this.$router.push("/Data/");
        })
        .catch((err) => {
          console.log(err);
        });
    },

    edit(inputd) {
      this.editdata = inputd[0];
      this.dialog1 = true;
      console.log("input selected : ", this.editdata.id);
      console.log("editdata selected : ", this.editdata);
    },

    async update() {
      this.dialog1 = false;
      console.log("edited data in update : ", this.editdata);

      await axios
        .put("http://localhost:3000/DATA1/" + this.editdata.id, this.editdata)
        .then((resp) => {
          console.log("Responce is : ", resp);
          this.getapicall();
        })
        .catch((err) => {
          console.log("Error : ", err);
        });
    },

    /**
     * Filter for calories column.
     * @param value Value to be tested.
     * @returns {boolean}
     */
    DTFilter(value) {
      // If this filter has no value we just skip the entire filter.
      if (!this.DTFilterValue) {
        return true;
      }

      // Check if the current loop value (The calories value)
      // equals to the selected value at the <v-select>.
      return value == this.DTFilterValue;
    },

    Selecteditm1() {
      console.log("value : ", this.DTFilterValue);
      this.path2 = "/Dashboard/";
      this.path2 = this.path2 + this.DTFilterValue;
      this.checkpointer1 = true;
      this.disableb = false;
    },
    dash2() {
      if (this.checkpointer1) {
        this.$router.push(this.path2);
      } else {
        this.$router.push(this.path1);
      }
    },

    gf1() {
      this.$refs.gearF1.click();
    },
    filechange1(event) {
      console.log("file1 : ", event.target.files[0].name);
      this.postdata.namegf1 = event.target.files[0].name;
      this.selectedfile = event.target.files[0];
      this.Sgf1 = true;

      this.geturl("gf1");
    },
    gf2() {
      this.$refs.gearF2.click();
    },
    filechange2(event) {
      console.log("file2 : ", event.target.files[0].name);
      this.postdata.namegf2 = event.target.files[0].name;
      this.selectedfile = event.target.files[0];
      this.Sgf2 = true;
      this.geturl("gf2");
    },
    gp1() {
      this.$refs.gearP1.click();
    },
    filechange3(event) {
      console.log("file3 : ", event.target.files[0].name);
      this.postdata.namegp1 = event.target.files[0].name;
      this.selectedfile = event.target.files[0];
      this.Sgp1 = true;
      this.geturl("gp1");
    },
    gp2() {
      this.$refs.gearP2.click();
    },
    filechange4(event) {
      console.log("file4 : ", event.target.files[0].name);
      this.postdata.namegp2 = event.target.files[0].name;
      this.selectedfile = event.target.files[0];
      this.Spf2 = true;
      this.geturl("gp2");
    },

    pf1() {
      this.$refs.pinionF1.click();
    },
    filechange5(event) {
      console.log("file5 : ", event.target.files[0].name);
      this.postdata.namepf1 = event.target.files[0].name;
      this.selectedfile = event.target.files[0];
      this.Spf1 = true;
      this.geturl("pf1");
    },
    pf2() {
      this.$refs.pinionF2.click();
    },
    filechange6(event) {
      console.log("file6 : ", event.target.files[0].name);
      this.postdata.namepf2 = event.target.files[0].name;
      this.selectedfile = event.target.files[0];
      this.Spf2 = true;
      this.geturl("pf2");
    },
    pp1() {
      this.$refs.pinionP1.click();
    },
    filechange7(event) {
      console.log("file7 : ", event.target.files[0].name);
      this.postdata.namepp1 = event.target.files[0].name;
      this.selectedfile = event.target.files[0];
      this.Spp1 = true;
      this.geturl("pp1");
    },
    pp2() {
      this.$refs.pinionP2.click();
    },
    filechange8(event) {
      console.log("file8 : ", event.target.files[0].name);
      this.postdata.namepp2 = event.target.files[0].name;
      this.selectedfile = event.target.files[0];
      this.Spp2 = true;
      this.geturl("pp2");
    },

    geturl(option) {
      const storage = getStorage();

      const metadata = {
        contentType: "image/jpeg",
      };

      // Create a reference to 'mountains.jpg'
      const mountainsRef = ref(storage, "data/" + this.selectedfile.name);

      const Task = uploadBytesResumable(
        mountainsRef,
        this.selectedfile,
        metadata
      );

      Task.on(
        "state_changed",
        (snapshot) => {
          // Get task progress, including the number of bytes uploaded and the total number of bytes to be uploaded
          const progress =
            (snapshot.bytesTransferred / snapshot.totalBytes) * 100;
          console.log("Upload is " + progress + "% done");
          switch (snapshot.state) {
            case "paused":
              console.log("Upload is paused");
              break;
            case "running":
              console.log("Upload is running");
              break;
          }
        },
        (error) => {
          // A full list of error codes is available at
          // https://firebase.google.com/docs/storage/web/handle-errors
          switch (error.code) {
            case "storage/unauthorized":
              // User doesn't have permission to access the object
              break;
            case "storage/canceled":
              // User canceled the upload
              break;

            // ...

            case "storage/unknown":
              // Unknown error occurred, inspect error.serverResponse
              break;
          }
        },
        () => {
          // Upload completed successfully, now we can get the download URL
          getDownloadURL(Task.snapshot.ref).then((downloadURL) => {
            console.log("option : ", option);

            if (option == "gf1") {
              this.postdata.GF1 = downloadURL;
            } else if (option == "gf2") {
              this.postdata.GF2 = downloadURL;
            } else if (option == "gp1") {
              this.postdata.GP1 = downloadURL;
            } else if (option == "gp2") {
              this.postdata.GP2 = downloadURL;
            } else if (option == "pf1") {
              this.postdata.PF1 = downloadURL;
            } else if (option == "pf2") {
              this.postdata.PF2 = downloadURL;
            } else if (option == "pp1") {
              this.postdata.PP1 = downloadURL;
            } else if (option == "pp2") {
              this.postdata.PP2 = downloadURL;
            } else {
              console.log("else block");
            }

            this.samurl = downloadURL;
            console.log("File available at : ", downloadURL);
          });
        }
      );
    },
  },
};

// filter: value => {
//             if (!this.calories && !this.sam) return true
//              // if(this.sam) return value > parseInt(this.sam)
//            if(this.calories && this.sam)

//            {
//              let S =value < parseInt(this.calories) && value>parseInt(this.sam)

//              return S}
//           },

// <div id="app">
//   <v-app id="inspire">
//     <div>
//       <v-data-table
//         :headers="headers"
//         :items="desserts"
//         item-key="name"
//         class="elevation-1"
//         :search="search"
//         :custom-filter="filterOnlyCapsText"
//       >
//         <template v-slot:top>
//           <v-text-field
//             v-model="search"
//             label="Search (UPPER CASE ONLY)"
//             class="mx-4"
//           ></v-text-field>
//         </template>
//         <template v-slot:body.append>
//           <tr>
//             <td></td>
//             <td>
//               <v-text-field
//                 v-model="calories"
//                 type="number"
//                 label="Less than"
//               ></v-text-field>
//             </td>
//              <td>
//               <v-text-field
//                 v-model="sam"
//                 type="number"
//                 label="greater than"
//               ></v-text-field>
//             </td>
//             <td colspan="4"></td>
//           </tr>
//         </template>
//       </v-data-table>
//     </div>
//   </v-app>
// </div>

// new Vue({
//   el: '#app',
//   vuetify: new Vuetify(),
//   data () {
//     return {
//       search: '',
//       calories: '',
//       sam:'',
//       desserts: [
//         {
//           name: 'Frozen Yogurt',
//           calories: 159,
//           fat: 6.0,
//           carbs: 24,
//           protein: 4.0,
//           iron: 1,
//         },
//         {
//           name: 'Ice cream sandwich',
//           calories: 237,
//           fat: 9.0,
//           carbs: 37,
//           protein: 4.3,
//           iron: 1,
//         },
//         {
//           name: 'Eclair',
//           calories: 262,
//           fat: 16.0,
//           carbs: 23,
//           protein: 6.0,
//           iron: 7,
//         },
//         {
//           name: 'Cupcake',
//           calories: 305,
//           fat: 3.7,
//           carbs: 67,
//           protein: 4.3,
//           iron: 8,
//         },
//         {
//           name: 'Gingerbread',
//           calories: 356,
//           fat: 16.0,
//           carbs: 49,
//           protein: 3.9,
//           iron: 16,
//         },
//         {
//           name: 'Jelly bean',
//           calories: 375,
//           fat: 0.0,
//           carbs: 94,
//           protein: 0.0,
//           iron: 0,
//         },
//         {
//           name: 'Lollipop',
//           calories: 392,
//           fat: 0.2,
//           carbs: 98,
//           protein: 0,
//           iron: 2,
//         },
//         {
//           name: 'Honeycomb',
//           calories: 408,
//           fat: 3.2,
//           carbs: 87,
//           protein: 6.5,
//           iron: 45,
//         },
//         {
//           name: 'Donut',
//           calories: 452,
//           fat: 25.0,
//           carbs: 51,
//           protein: 4.9,
//           iron: 22,
//         },
//         {
//           name: 'KitKat',
//           calories: 518,
//           fat: 26.0,
//           carbs: 65,
//           protein: 7,
//           iron: 6,
//         },
//       ],
//     }
//   },
//   computed: {
//     headers () {
//       return [
//         {
//           text: 'Dessert (100g serving)',
//           align: 'start',
//           sortable: false,
//           value: 'name',
//         },
//         {
//           text: 'Calories',
//           value: 'calories',
//           filter: value => {
//             if (!this.calories && !this.sam) return true
//              // if(this.sam) return value > parseInt(this.sam)
//            if(this.calories && this.sam)

//            {
//              let S =value < parseInt(this.calories) && value>parseInt(this.sam)

//              return S}
//           },
//         },
//         { text: 'Fat (g)', value: 'fat' },
//         { text: 'Carbs (g)', value: 'carbs' },
//         { text: 'Protein (g)', value: 'protein' },
//         { text: 'Iron (%)', value: 'iron' },
//       ]
//     },
//   },
//   methods: {
//     filterOnlyCapsText (value, search, item) {
//       return value != null &&
//         search != null &&
//         typeof value === 'string' &&
//         value.toString().toLocaleUpperCase().indexOf(search) !== -1
//     },
//   },
// })












</script>
