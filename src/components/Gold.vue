<template>
    <div class="box">
        <h2>ดึงราคาทองคำผ่าน API</h2>
        <button @click="fetchGold" class="btn-refresh">🔄 รีเฟรชข้อมูลราคาทอง</button>

        <div v-if="loading" style="margin-top: 15px; color: #666;">กำลังโหลดข้อมูล...</div>

        <div v-else-if="gold" class="gold-box">
            <h3 style="margin-top: 0; color: #b78103;">📌 ราคาทองคำประจำวัน</h3>
            <p style="font-size: 14px; color: #555;">
                วันที่: <strong>{{ gold.update_date }}</strong> | เวลา: <strong>{{ gold.update_time }}</strong>
            </p>
            <hr style="border: 0; border-top: 1px solid #e0e0e0;">
            
            <h4>ทองคำแท่ง</h4>
            <div class="price-item">ราคารับซื้อ: <strong style="color: green;">{{ gold.price.gold_bar.buy }} บาท</strong></div>
            <div class="price-item">ราคาขายออก: <strong style="color: red;">{{ gold.price.gold_bar.sell }} บาท</strong></div>

            <h4 style="margin-top: 15px;">ทองรูปพรรณ</h4>
            <div class="price-item">ราคารับซื้อ: <strong style="color: green;">{{ gold.price.gold.buy }} บาท</strong></div>
            <div class="price-item">ราคาขายออก: <strong style="color: red;">{{ gold.price.gold.sell }} บาท</strong></div>
        </div>

        <div v-if="errorText" style="color: red; margin-top: 15px;">
            {{ errorText }}
        </div>
    </div>
</template>

<script>
export default {
    name: 'Gold',
    data() {
        return {
            gold: null,
            loading: false,
            errorText: ''
        }
    },
    methods: {
        async fetchGold() {
            this.loading = true;
            this.errorText = '';
            try {
                const res = await fetch('https://api.chnwt.dev/thai-gold-api/latest');
                const data = await res.json();

                if (data.status === 'success' && data.response) {
                    this.gold = data.response;
                } else {
                    this.errorText = 'รูปแบบข้อมูล API ไม่ถูกต้อง';
                }
            } catch (err) {
                console.error(err);
                this.errorText = 'ไม่สามารถเชื่อมต่อ API ได้';
            } finally {
                this.loading = false;
            }
        }
    },
    mounted() {
        this.fetchGold();
    }
}
</script>

<style scoped>
.box {
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}
.btn-refresh {
    background-color: #ffc107;
    border: none;
    padding: 8px 12px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
}
.gold-box {
    background: #fffdf0;
    border: 1px solid #ffeeba;
    padding: 15px;
    border-radius: 6px;
    margin-top: 15px;
}
.price-item {
    margin: 8px 0;
    font-size: 16px;
}
</style>