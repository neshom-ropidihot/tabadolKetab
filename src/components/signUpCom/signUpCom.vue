<template>
  <v-row no-gutters class="justify-center">
    <v-col cols="12" sm="6" md="8">
      <v-card class="pa-4">
        <v-card-actions class="teal">
          <v-card-title class="white--text pa-0">
            <span>
              {{ $t('signUp') }}
            </span>
          </v-card-title>
        </v-card-actions>

        <v-form class="pt-6" ref="form" v-model="valid">
          <v-container>
            <v-row>
              <v-col cols="12" md="6">
                <v-text-field
                  v-model="register.firstName"
                  :rules="nameRules"
                  :label="$t('name')"
                  required
                  outlined
                  autofocus
                  error-count="2"
                ></v-text-field>
              </v-col>
              <v-col cols="12" md="6">
                <v-text-field
                  v-model="register.lastName"
                  :rules="nameRules"
                  :label="$t('lastName')"
                  required
                  outlined
                  error-count="2"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" md="6">
                <nationalId />
              </v-col>
              <v-col cols="12" md="6">
                <mobilePhone />
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12" md="6">
                <v-text-field
                  v-model="register.phone"
                  :rules="nameRules"
                  :label="$t('phone')"
                  required
                  outlined
                  error-count="2"
                ></v-text-field>
              </v-col>
              <v-col cols="12" md="6">
                <v-select
                  :items="introductionType"
                  :label="$t('introduction')"
                  outlined
                  clearable
                  hide-selected
                >
                  <template v-slot:item="{ item }">
                    <span>
                      {{ $t(item) }}
                    </span>
                  </template>
                  <template v-slot:selection="{ item }">
                    <span>
                      {{ $t(item) }}
                    </span>
                  </template>
                </v-select>
              </v-col>
            </v-row>
            <passwords />
            <v-checkbox
              v-model="register.rules"
              required
              color="success"
              class="col-6 col-md-4"
            >
              <template v-slot:label>
                <div>
                  من
                  <v-tooltip bottom>
                    <template v-slot:activator="{ on }">
                      <a
                        target="_blank"
                        href="http://vuetifyjs.com"
                        @click.stop
                        v-on="on"
                      >
                        قوانین
                      </a>
                    </template>
                    مطالعه قوانین سایت
                  </v-tooltip>
                  سایت را قبول می نمایم
                </div>
              </template>
            </v-checkbox>
            <captcha />
            <div class="justify-center d-flex">
              <v-btn
                :disabled="!valid"
                color="success"
                class="mr-4"
                @click="validate"
              >
                {{ $t('save') }}
              </v-btn>

              <v-btn color="error" class="mr-4" @click="reset"
                >{{ $t('resetForm') }}
              </v-btn>
            </div>
          </v-container>
        </v-form>
      </v-card>
    </v-col>
    <successNotif
      v-if="saveSuccess"
      :msg="'operationSuccessfullyOcured'"
      @hideNotif="hideNotif"
    />
  </v-row>
</template>

<script>
import successNotif from '../structure/successNotif.vue';
import passwords from '../userControls/passwords.vue';
import mobilePhone from '../userControls/mobilePhone.vue';
import nationalId from '../userControls/nationalId.vue';
import captcha from '../userControls/captch.vue';

export default {
  name: 'signUpCom',
  components: {
    successNotif,
    passwords,
    mobilePhone,
    nationalId,
    captcha,
  },
  data() {
    return {
      saveSuccess: false,
      valid: true,
      nameRules: [
        v => !!v || `${this.$t('thisFieldIsRequired')}`,
        v => (v && v.length >= 3) || `${this.$t('minCharaters3')}`,
      ],
      introductionType: [
        'website',
        'advertising',
        'friendsAndAcquaintances',
        'other',
      ],
      register: {
        firstName: '',
        lastName: '',
        phone: '',
        introductionType: null,
        rules: false,
      },
    };
  },
  methods: {
    validate() {
      this.$refs.form.validate();
      if (this.$refs.form.validate()) {
        this.saveSuccess = true;
        this.reset();
        console.log('ok');
      } else {
        this.valid = false;
      }
    },
    reset() {
      this.$refs.form.reset();
    },
    // notif hide
    hideNotif() {
      this.saveSuccess = false;
    },
  },
};
</script>

<style lang="scss"></style>
