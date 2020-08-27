<template>
    <div class="menubarr">
    <nav class="sidebar">
      <header>Наша клиника</header>
        <a href="#">
          <span>Главная</span>
        </a>
        <a href="#">
          <span>График работы</span>
        </a>
        <a href="#">
          <span>Список врачей</span>
        </a>
        <a href="#">
          <span>Список клиентов</span>
        </a>
        <a href="#" class="active">
          <span>Новый клиент</span>
        </a>
        <a href="#">
          <span>Настройки</span>
        </a>
      
    </nav>
    </div>
</template>

<style lang="scss">
.sidebar{
  position: fixed;
  width: 300px;
  left: 0px;
  height: 100%;
  background: #042331;

 header{
  font-size: 28px;
  color: white;
  line-height: 70px;
  text-align: center;
  background: #063146;
  user-select: none;

}
 a{
  display: block;
  height: 65px;
  width: 100%;
  color: white;
  line-height: 65px;
  padding-left: 30px;
  box-sizing: border-box;
  border-bottom: 1px solid black;
  border-top: 1px solid rgba(255,255,255,.1);
  border-left: 5px solid transparent;

}
a.active,a:hover{
  border-left: 5px solid #005b88;
  color: #005b88;
}
 a {
  span{
  letter-spacing: 1px;
  text-transform: uppercase;
}
 }
}
@media(max-width : 900px){
  .sidebar{
    width: 100%;
    z-index: 1;
    display: inline-flex;
    height: auto;

    header {
      display: none;
    }

    a{
      padding: 10px;
      line-height: 20px;
      border-left: 0px;
      height: 50px;

     
      span{
       letter-spacing: 0px;
       text-transform: none;
       position: absolute;
       width: 20px;
       font-size: 20px;
       margin: 0px 20px;
      }
    }
    a.active,a:hover{
      border-left: none;
      border-bottom: 5px solid #005b88;
      color: #005b88;
    }
  }
    a:hover {
      background: inherit;
    }
    .sidebar a:hover span{
    opacity: 1;
    visibility: visible;
  }
}
@media(max-width : 768px){
  .sidebar{
    a{      
      span{
        font-size: 16px;
        margin: 0px;
      }
    }
  }
}
@media(max-width : 550px){
  .sidebar{
    a{      
      span{
        font-size: 12px;
      }
    }
  }
}
</style>

