<template>
    <div class="box">
        <h2>โปรแกรมตัดเกรด</h2>
        <label>กรอกคะแนน (0-100):</label><br>
        <input type="number" v-model.number="score" placeholder="ใส่คะแนนตรงนี้"><br>

        <div v-if="score !== null && score !== ''" class="result">
            <p>คะแนน: <strong>{{ score }}</strong></p>
            <p>เกรดที่ได้: <strong style="color: blue;">{{ grade }}</strong></p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Grade',
    data() {
        return {
            score: null
        }
    },
    computed: {
        grade() {
            if (this.score === null || this.score === '') return '';
            if (this.score >= 80) return 'A';
            if (this.score >= 75) return 'B+';
            if (this.score >= 70) return 'B';
            if (this.score >= 65) return 'C+';
            if (this.score >= 60) return 'C';
            if (this.score >= 55) return 'D+';
            if (this.score >= 50) return 'D';
            return 'F';
        }
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
input {
    width: 90%;
    padding: 8px;
    margin: 10px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
}
.result {
    margin-top: 15px;
    padding: 10px;
    background: #f9f9f9;
    border-radius: 4px;
}
</style>