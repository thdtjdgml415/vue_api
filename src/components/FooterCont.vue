<template>
  <footer id="footer">
    <div className="footer__inner">
      <div>
        <h3>email</h3>
        <a href="mailto:thdtjdgml415@naver.com">thdtjdgml415@naver.com</a>
      </div>
      <div>
        <h3>kakao</h3>
        <a href="/">songdh9</a>
      </div>
      <div>
        <h3>social</h3>
        <ul>
          <li>
            <a href="/">youtube</a>
          </li>
          <li>
            <a href="/">favebook</a>
          </li>
          <li>
            <a href="/">instagram</a>
          </li>
        </ul>
      </div>
    </div>
  </footer>
</template>

<style lang="scss">
.footer__inner {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  background-color: var(--bg-dark);
  color: var(--white);
  border-top: 1px solid var(--bg-dark-border);
  display: flex;
  align-items: center;
  font-family: var(--font-sub2);
  z-index: 100;

  div {
    text-align: center;
    &:nth-child(1) {
      flex: 1 1 40%;
      border-right: 1px solid var(--bg-dark-border);
    }
    &:nth-child(2) {
      flex: 1 1 30%;
      border-right: 1px solid var(--bg-dark-border);
    }
    &:nth-child(3) {
      flex: 1 1 40%;
    }
  }
  h3 {
    padding: 20px;
  }
  h3,
  ul,
  li {
    display: inline-block;
  }
  a {
    display: inline-block;
    margin: 20px;
    color: var(--white);
    opacity: 0.6;
    position: relative;
    transition: opacity 0.3s;
    text-transform: capitalize;
    &:hover {
      opacity: 1;
    }
    &::before {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0;
      width: 100%;
      height: 1px;
      background: var(--white);
      transform: scaleX(0);
      transition: all 0.3s ease;
    }
    &:hover::before {
      transform: scaleX(1);
    }
  }
}
</style>
