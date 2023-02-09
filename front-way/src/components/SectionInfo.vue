<template>
  <div class="section-info">
    <div class="section-content">
      <ul class="data-item">
        <li class="item">
          <box-icon name="book-bookmark" color="#42b983" size="60px"></box-icon
          >Отчетов сформировано<span class="item-volume">10600</span>
        </li>
        <li class="item">
          <box-icon name="user-pin" color="#42b983" size="60px"></box-icon
          >Численность работников<span class="item-volume">13783</span>
        </li>
        <li class="item">
          <box-icon name="building-house" color="#42b983" size="60px"></box-icon
          >Количество групп<span class="item-volume">737</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SectionInfo'
}
</script>

<style>
.section-content {
  position: relative;
  margin: 0;
  padding: 20px 30px;
  display: flex;
  box-sizing: border-box;
  border: 1rem solid rgba(0, 0, 0, 0.1);
  width: 95%;
  margin: auto;
}

.data-item {
  padding: 0;
  margin: 0;
  display: flex;
  align-items: center;
  box-sizing: border-box;
  flex-wrap: wrap;
}

.item {
  padding-right: 30px;
  display: flex;
  justify-content: space-between;
  font-size: 1rem;
  word-wrap: break-word;
  text-align: left;
  align-items: center;
  box-sizing: border-box;
}

.item:last-child {
  padding: 0;
}

.item-volume {
  font-size: 1.2rem;
  font-weight: 900;
  padding-left: 30px;
}

ul {
  list-style-type: none;
}

@media only screen and (max-width: 576px){
.section-content {
  padding: 10px 20px;
}
.item {
  padding: 0;
  font-size: 0.8rem;
}
.item-volume {
  font-size: 1rem;
}
}
</style>
