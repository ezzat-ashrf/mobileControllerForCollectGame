# Samsung mobile controller

The Firebase project is configured in `index.html`. It writes to `devices/samsung-screen-01/control`.

Run locally with `python -m http.server 8080`, then open `http://localhost:8080`.

Hold left or right to move the basket. Releasing sends `horizontal: 0`. The small bottom dot is green when Firebase is reachable and red when it is not.
