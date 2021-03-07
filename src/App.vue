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
                    <v-col cols="12" xs="10" sm="9" md="9">
                      <v-text-field
                        required
                        label="Фамилия и имя"
                        v-model="fullName"
                        hint="К примеру: Шипулин Сергей"
                      >
                      </v-text-field>
                    </v-col>
                  </v-row>
                  <v-row class="justify-center text-center">
                    <v-col cols="12" xs="6" sm="8" md="5">
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
      <v-container>
        <!-- Исключение со мной -->
        <div v-if="fullName == 'Шипулин Сергей'">
          <v-row class="text-center">
            <v-col>
              <v-alert color="red" dark border="left">
                <h2>
                  Не ну, Вы серьёзно? Вы хотите, чтобы я и себя поздравил?
                </h2>
              </v-alert>
            </v-col>
          </v-row>
        </div>

        <!-- Пацаны со списка -->
        <div
          v-else-if="
            fullName == 'Сергиенко Андрей' ||
            fullName == 'Наурузов Карим' ||
            fullName == 'Айкимбаев Максат' ||
            fullName == 'Селибаев Гизат' ||
            fullName == 'Агафонов Андрей'
          "
        >
          <v-row>
            <v-col>
              <v-alert border="left" colored-border elevation="2">
                <h1>
                  Пацаны, я не умею придумывать поздравления для вас, на 8
                  марта! Так что простить и жаловать
                </h1>
              </v-alert>
            </v-col>
          </v-row>

          <v-row>
            <v-col>
              <v-alert class="text-left" type="success"
                >Особое поздравление</v-alert
              >
            </v-col>
          </v-row>
          <div v-for="list in lists" v-bind:key="list.name">
            <v-row class="justify-center">
              <v-col cols="8">
                <div v-if="fullName == list.name">
                  <v-card elevation="1">
                    <v-card-title> Поздравляю, {{ name[1] }} </v-card-title>
                    <v-card-subtitle class="yellow--text text--darken-4">Это особое поздравление, сделанное, специально мною</v-card-subtitle>
                    <v-card-text class="black--text">{{list.congratulation}}</v-card-text>
                  </v-card>
                </div>
              </v-col>
            </v-row>
          </div>
        </div>

        <div
          v-else-if="
            fullName == 'Дуйсенбекова Анель' ||
            fullName == 'Султангазина Махфуза'
          "
        >
          <v-row>
            <v-col>
              <v-alert border="left" dark color="indigo">
                <h1>
                  Поздравляю
                  <span class="deep-orange--text">{{ name[1] }}</span> с 8
                  марта!
                </h1>
              </v-alert>
              <h2>Дарю цветы от меня) 💐</h2></v-col
            >
          </v-row>
        </div>

        <div v-else>
          <v-row>
            <v-col>
              <v-alert
                border="left"
                color="orange"
                class="white--text"
                dismissible
              >
                <h1>
                  Если ты видешь и читаешь это, то тебя видимо нет в списке :(
                </h1>
              </v-alert>
            </v-col>
          </v-row>

          <div v-if="!MaleChoice && !WomanChoice">
            <v-row
              ><v-col><h2>Ответь на вопрос, какого пола ты?</h2></v-col></v-row
            >
            <v-row>
              <v-col
                ><v-btn class="mx-2 green white--text" v-on:click="maleChoice"
                  >Мужской</v-btn
                >
                <v-btn class="mx-2 red white--text" v-on:click="womanChoice"
                  >Женский</v-btn
                ></v-col
              >
            </v-row>
          </div>

          <v-row v-if="MaleChoice">
            <v-col> Чел, ну ты как бы, мужик</v-col>
          </v-row>

          <v-row v-if="WomanChoice">
            <v-col> Ты Баба </v-col>
          </v-row>
        </div>
      </v-container>
    </div>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      dialog: true,
      fullName: "Марипбеков Чингиз",
      name: "",
      congratulation: false,
      lists: [
        { name: " Султангазина Махфуза", congratulation: "" },
        { name: "Дуйсенбекова Анель", congratulation: "" },
        { name: "Сергиенко Андрей", congratulation: "Так, Андрей, который Сергиенко, пока вспоминал твою фамилию, выпил 2 чашки кофе, поверх принял антидепрессант, но короче, с Международным Женским Днём" },
        { name: "Наурузов Карим", congratulation: "Карим, бро. С 8 марта тебя, желаю я тебе всего наилучшего в этот день, да и в жизни (заебался я писать уникальные поздравления )" },
        { name: "Айкимбаев Максат", congratulation: "Махат, даже здесь, я хочу оскорбить тебя и да я это сделаю, но сначало, с твоим праздником, ты же его ждал целых 366 дней, ну так вот, сегодня не буду оскорблядь" },
        { name: "Селибаев Гизат", congratulation: "Гизат, ну ты не смог придумать для себя поздравление, поэтому я сам придумал. Так вот, пусть тебе случайно перекинуть 10К на каспи, да и всего хорошего тебе" },
        { name: "Агафонов Андрей", congratulation: "Back-end-эр команды, я не умею говорить яркии и запоминающие поздравления, но в пару слов я могу поздравить о тебе. Так вот хорошего тебе всего в День всех Женщин, не так красочно я как я себе представлял всё" },
      ],

      MaleChoice: false,
      WomanChoice: false,
    };
  },

  methods: {
    // Показать пришлашение
    showCongratulation() {
      this.dialog = false;
      this.congratulation = true;
      this.name = this.fullName.split(" ");
    },

    // Выбор мужского пола
    maleChoice() {
      this.MaleChoice = true;
    },

    // Выбор женского пола
    womanChoice() {
      this.WomanChoice = true;
    },
  },
};
</script>

