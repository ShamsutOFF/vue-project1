<template>
  <div class="card">
    <div class="card-header">
      <div class="card-number">09</div>
    </div>
    <div class="card-content">
      <div class="card-text">oscillotron</div>
    </div>
    <div class="card-footer">
      ПЕРЕВЕНУТЬ
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 250px;
  height: 380px;
  border-radius: 16px;
  background-color: var(--color-white);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  position: relative;
  overflow: hidden;
  transition: transform 0.3s ease;
  transform-style: preserve-3d;
  box-shadow: 0 0 16px 0 #0000001A;
}

.card::before {
  content: '';
  position: absolute;
  top: 27px;
  left: 19px;
  right: 19px;
  bottom: 27px;
  border: 1px solid var(--color-light-blue);
  border-radius: 8px;
  pointer-events: none;
  z-index: 1;
}

.card:hover {
  cursor: pointer;
  transform: scale(1.01);
  box-shadow: 10px 10px 10px 0 #0000000D;
}

.card-header {
  width: 100%;
  text-align: left;
  position: relative;
  z-index: 2;
  box-sizing: border-box;
  padding-left: 32px;
  padding-top: 16px;
}

.card-number {
  background-color: var(--color-white);
  font-size: 14px;
  padding: 2px;
  line-height: 100%;
  font-weight: 400;
  color: var(--color-text-main);
  display: inline-block;
}

.card-content {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  position: relative;
  z-index: 2;
}

.card-text {
  font-size: 18px;
  text-align: center;
  line-height: 100%;
  font-weight: 400;
  color: var(--color-text-main);
}

.card-footer {
  background-color: var(--color-white);
  padding-bottom: 18px;
  padding-left: 4px;
  padding-right: 4px;
  text-align: center;
  font-weight: 700;
  font-size: 12px;
  line-height: 18px;
  letter-spacing: 2px;
  color: var(--color-text-main);
  position: relative;
  z-index: 2;
}
</style>
