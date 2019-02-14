<template>
  <v-dialog v-model="dialog" persistent max-width="600px">
    <v-btn flat slot="activator">
        <span class="mr-2">Войти</span>
    </v-btn>
    <v-tabs
      v-model="active"
      color="blue"
      dark
      height="70px"      
      slider-color="yellow"
    >
      <v-tab :key="0" ripple>Вход</v-tab>
      <v-tab :key="1" ripple>Регистрация</v-tab>
      <v-tab-item :key="0">
        <v-card flat>
          <v-card-text>...</v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn flat @click="dialog = false">Отмена</v-btn>
            <v-btn disabled @click="dialog = false">Войти</v-btn>
          </v-card-actions>          
        </v-card>
      </v-tab-item>
      <v-tab-item :key="1">
        <v-card flat>
          <v-card-text>
          <v-form
            ref="signForm"
            v-model="signValid"            
          >
            <v-text-field
              v-model="name"
              :counter="20"
              :rules="nameRules"
              label="ИМЯ"
              required
            ></v-text-field>

            <v-text-field
              v-model="email"
              :rules="emailRules"
              label="E-MAIL"
              required
            ></v-text-field>
            <v-text-field
              v-model="password"
              :append-icon="showPassword ? 'visibility_off' : 'visibility'"
              :rules="[v => v.length >= 6 || 'Минимум 6 символов']"
              :type="showPassword ? 'text' : 'password'"
              label="ПАРОЛЬ"
              hint="Минимум 6 символов"
              counter
              @click:append="showPassword = !showPassword"
            ></v-text-field>            
            <v-checkbox
              v-model="checkbox"
              :rules="[v => !!v || 'Вы должны согласиться с правилами для продолжения!']"
              label="Я согласен с правилами сервиса."
              required
            ></v-checkbox>         
          </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn flat @click="dialog = false">Отмена</v-btn>            
            <v-btn 
              :disabled="!signValid"
              @click="dialog = false">Регистрация</v-btn>
          </v-card-actions>
        </v-card>
      </v-tab-item>
    </v-tabs>
<!--        
        <v-container grid-list-md>
          <v-layout wrap>
            <v-flex xs12 sm6 md4>
              <v-text-field label="Legal first name*" required></v-text-field>
            </v-flex>
            <v-flex xs12 sm6 md4>
              <v-text-field label="Legal middle name" hint="example of helper text only on focus"></v-text-field>
            </v-flex>
            <v-flex xs12 sm6 md4>
              <v-text-field
                label="Legal last name*"
                hint="example of persistent helper text"
                persistent-hint
                required
              ></v-text-field>
            </v-flex>
            <v-flex xs12>
              <v-text-field label="Email*" required></v-text-field>
            </v-flex>
            <v-flex xs12>
              <v-text-field label="Password*" type="password" required></v-text-field>
            </v-flex>
            <v-flex xs12 sm6>
              <v-select
                :items="['0-17', '18-29', '30-54', '54+']"
                label="Age*"
                required
              ></v-select>
            </v-flex>
            <v-flex xs12 sm6>
              <v-autocomplete
                :items="['Skiing', 'Ice hockey', 'Soccer', 'Basketball', 'Hockey', 'Reading', 'Writing', 'Coding', 'Basejump']"
                label="Interests"
                multiple
              ></v-autocomplete>
            </v-flex>
          </v-layout>
        </v-container>
        <small>*indicates required field</small>
-->        
<!--
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue darken-1" flat @click="dialog = false">Close</v-btn>
        <v-btn color="blue darken-1" flat @click="dialog = false">Save</v-btn>
      </v-card-actions>
    </v-card>-->
  </v-dialog>
</template>
<script>
  export default {
    data: () => ({
      active: 0,
      dialog: false,

      name: '',
      password: '',
      showPassword: false,
      nameRules: [
        v => !!v || 'Имя обязательно',
        v => (v && v.length >= 6) || 'Минимум 6 символов'
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail обязателен',
        v => /.+@.+/.test(v) || 'Некорректный e-mail'
      ],
      checkbox: false,
      signValid: false    
    }),
    methods: {
      signIn() {
        firebase.auth().createUserWithEmailAndPassword(this.email, this.password).catch(function(error) {
          var errorCode = error.code;
          var errorMessage = error.message;
          // ...
        });
      }
    }
  }
</script>