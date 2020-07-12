<template>
<div>
  <div class="meter_value">{{ value | toFixed(2) }} <span>{{ unit }}</span></div>
</div>
</template>

<script>
export default {
    name: 'MeterValue',
    props: {
        value: Number,
        unit: String
    },
    filters: {
        toFixed: function(val, round) {
            return Number(val).toFixed(round);
        },
    },
}
</script>

<style scoped>
.meter_value {
    color: #444444;
    font-size: 6rem;
    font-weight: bold;
    line-height: 1;
}
</style>
