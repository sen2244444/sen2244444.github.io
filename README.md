<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css" integrity="sha512-Evv84Mr4kqVGRNSgIGL/F/aIDqQb7xQ2vcrdIwxfjThSH8CSR7PBEakCr51Ck+w+/U6swU2Im1vVX0SVk9ABhg==" crossorigin="anonymous" referrerpolicy="no-referrer" />
  <link rel="stylesheet" href="style.css" />
  <title>NAVBAR MALAIKAT</title>
</head>

<body>
  <main>
    <section class="screen">
      <div class="parent-navbar">
        <div class="navbar">
          <div class="nav-item" data-index="1">
            <i class="icon-item fa-solid fa-house"></i>
          </div>
          <div class="nav-item" data-index="2">
            <i class="icon-item fa-solid fa-message"></i>
          </div>
          <div class="nav-item" data-index="3">
            <i class="icon-item fa-brands fa-windows"></i>
          </div>
          <div class="nav-item" data-index="4">
            <i class="icon-item fa-solid fa-user"></i>
          </div>
          <div class="bullet" style="--bullet-index: 1">
            <div class="bullet-inside"></div>
          </div>
        </div>
      </div>
    </section>
  </main>
  <script src="script.js"></script>
</body>

</html>

main {
  display: flex;
  justify-content: center;
}
.screen {
  height: 80vh;
  width: 300px;
  border: 1px solid black;
  background-color: rgb(4, 0, 65);
  position: relative;
  border-radius: 15px;
  margin: 10px;
  overflow: hidden;
}
.parent-navbar {
  position: absolute;
  bottom: 0;
  width: 100%;
}
.navbar {
  background-color: white;
  display: flex;
  position: relative;
  bottom: 0;
  width: 100%;
  border-radius: 15px;
  justify-content: space-around;
Ï
}
.nav-item {
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.nav-item .icon-item {
    transition: all 0.5s ease-in-out;
}

.bullet {
  width: 50px;
  position: absolute;
  background-color: rgb(4, 0, 65);
  border-radius: 50%;
  height: 50px;
  top: -50%;
  left: calc(5% + (var(--bullet-index) - 1) * 25%);
  transition: left 0.5s ease;
  display: flex;
  justify-content: center;
  align-items: center;
  /* 5 , 30, 55, 80 */
}

.bullet-inside {
  background-color: white;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.bullet-inside::before {
  content: '';
  width: 20px;
  height: 20px;
  background-color: transparent;
  position: absolute;
  right: 100%;
  bottom: 0;
  border-top-right-radius: 9999px;
  box-shadow: 0px -9px 0 0 rgb(4, 0, 65);
  border: 0px solid transparent;
}
.bullet-inside::after {
  content: '';
  width: 20px;
  height: 20px;
  background-color: transparent;
  position: absolute;
  left: 100%;
  bottom: 0;
  border-top-left-radius: 9999px;
  box-shadow: 0px -9px 0 0 rgb(4, 0, 65);
}

const navItems = document.querySelectorAll(".nav-item");
const bullet = document.querySelector(".bullet");

const firstIcon = navItems[0].querySelector(".icon-item");
firstIcon.style.zIndex = "99";
firstIcon.style.transform = "translateY(-150%)";

navItems.forEach((item, index) => {
  item.addEventListener("click", function () {
    const dataIndex = item.getAttribute("data-index");

    bullet.style.setProperty("--bullet-index", dataIndex);

    navItems.forEach((navItem, idx) => {
      const icon = navItem.querySelector(".icon-item");
      icon.style.zIndex = "";
      icon.style.transform = "";
    });

    const icon = item.querySelector(".icon-item");
    icon.style.zIndex = "99";
    icon.style.transform = "translateY(-150%)";
  });
});
Ï;
