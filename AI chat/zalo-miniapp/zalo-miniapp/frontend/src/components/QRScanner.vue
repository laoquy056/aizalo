<template>
  <div>
    <h2>Quét mã QR</h2>
    <qrcode-stream @decode="onScanSuccess" />
    <p v-if="qrData">Dữ liệu QR: {{ qrData }}</p>
  </div>
</template>

<script>
import { QrcodeStream } from 'vue-qrcode-reader';
import axios from 'axios';

export default {
  components: { QrcodeStream },
  data() {
    return { qrData: '' };
  },
  methods: {
    async onScanSuccess(data) {
      this.qrData = data;
      const response = await axios.post('http://localhost:8000/check-qr', { qr_code: data });
      alert(response.data.exists ? "QR Hợp lệ!" : "QR Không tồn tại!");
    }
  }
};
</script>
