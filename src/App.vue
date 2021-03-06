<template>
  <v-app>
    <div>
      <v-dialog persistent v-model="dialog">
        <v-card>
          <v-card-text>
            <div>
              <v-container>
                <v-row class="text-center">
                  <v-col>
                    <h1 class="display-2 mt-5">
                      <span class="green--text">С</span>
                      <span class="blue--text"> 8 </span>
                      <span class="red--text">марта</span>
                      <span> 💐💐💐</span>
                    </h1>
                  </v-col>
                </v-row>

                <v-form v-on:submit.prevent="showCongratulation">
                  <v-row class="justify-center">
                    <v-col cols="6" xs="10" sm="9" md="5">
                      <v-text-field
                        required
                        label="Фамилия и имя"
                        v-model="fullName"
                      >
                      </v-text-field>
                    </v-col>
                  </v-row>
                  <v-row class="justify-center text-center">
                    <v-col cols="6" xs="6" sm="8" md="5">
                      <v-btn
                        v-on:click="showCongratulation"
                        block
                        color="success"
                        >Получить поздравление</v-btn
                      >
                    </v-col>
                  </v-row>
                </v-form>
              </v-container>
            </div>
          </v-card-text>
        </v-card>
      </v-dialog>
    </div>

    <div v-if="congratulation == true">
      <v-container v-for="list in lists" :key="list.name">
        <v-row>
          <v-col cols="12" v-if="list.name == fullName">
            <h1>Поздравляю тебя с 8 марта {{ name[0] }}</h1>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      dialog: true,
      fullName: "",
      name: "",
      congratulation: false,
      lists: [
        { name: "Шипулин Сергей", congratulation: "Ты серьёзно?" },
        { name: "Сергиенко Андрей", congratulation: "" },
      ],
    };
  },

  methods: {
    showCongratulation() {
      this.dialog = false;
      this.congratulation = true;
      this.name = this.fullName.split(" ");
    },
  },
};
</script>
