<template>
  <v-row no-gutters class="justify-center ">
    <v-col cols="12" sm="8" md="8">
      <v-card>
        <v-card-actions class="teal"> </v-card-actions>
        <div class="pa-4 clear">
          <div class="float-right">
            <v-icon>
              mdi-book-open-page-variant
            </v-icon>
            <span class="pr-4 font-weight-bold"> {{ ticket.title }}</span>
          </div>
          <div class="float-left">
            <p class="sendDateP">
              {{ $t('sendDate') }}
            </p>
            <span>
              {{ new Date(ticket.sendDate).toLocaleTimeString('fa') }}
              <v-icon small color="red">
                mdi-clock
              </v-icon>
              {{ new Date(ticket.sendDate).toLocaleDateString('fa') }}
              <v-icon small color="black">
                mdi-calendar
              </v-icon>
            </span>
          </div>
          <div class="ticketSender">
            <span class="red--text text--darken-4">
              <v-icon medium color="red darken-2">
                mdi-account
              </v-icon>
              <span class="pr-4">
                {{ ticket.sender.firstName }}
                &nbsp;
                {{ ticket.sender.lastName }}
              </span>
            </span>
          </div>
        </div>
      </v-card>
      <template v-for="item in ticket.threads">
        <threadEncapsule :key="item.index" :data="item" />
      </template>
      <ticketReply :key="componentKey" @replyTicket="replyTicket" />
    </v-col>
    <successNotif
      v-if="successNotif"
      :msg="'operationSuccessfullyOcured'"
      @hideNotif="hideNotif"
    />
  </v-row>
</template>

<script>
import threadEncapsule from './threadEncapsule.vue';
import ticketReply from './ticketReply.vue';
import successNotif from '../structure/successNotif.vue';

export default {
  name: 'ticketCmp',
  components: {
    threadEncapsule,
    ticketReply,
    successNotif,
  },
  data() {
    return {
      componentKey: 0,
      successNotif: false,
      ticket: {
        title: 'برای ایجاد فلان کار لطفا بخش فلان را مشاهده فرمایید',
        sendDate: '2020-10-16T16:45:28.149Z',
        sender: {
          firstName: 'علی',
          lastName: 'تبادلیان',
          role: 'client',
          id: '1234',
        },
        threads: [
          {
            id: '1',
            description:
              'برای انجام این کار مجموعه تبادل مستلزم کار فلان زمان است ، متاسفانه امکان انجام آن وجود ندارد',
            createdAt: '2020-10-16T16:45:28.149Z',
            createdBy: {
              id: '1234',
              firstName: 'علی',
              lastName: 'تبادلیان',
              role: 'client',
              avatar: {},
            },
          },
          {
            id: '2',
            description:
              'برای انجام این کار مجموعه تبادل مستلزم کار فلان زمان است ، متاسفانه امکان انجام آن وجود ندارد',
            createdAt: '2020-10-16T16:45:28.149Z',
            createdBy: {
              id: '1234',
              firstName: 'علی',
              lastName: 'تبادلیان',
              role: 'staff',
              avatar: {},
            },
          },
        ],
      },
    };
  },
  methods: {
    replyTicket(value) {
      console.log(value);
      console.log('ticket reply sent!');
      this.componentKey = +1;
      this.successNotif = true;
    },
    // notif
    hideNotif() {
      this.successNotif = false;
    },
  },
};
</script>

<style lang="scss">
.sendDateP {
  border-bottom: thin solid #bff7e9;
  padding: 6px;
  margin: 0;
  margin-bottom: 4px !important;
  text-align: center;
  font-size: 12px;
  color: #009572;
}
.ticketSender {
  width: 100%;
  float: right;
}
</style>
