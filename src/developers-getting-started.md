# Get started

This page describes how to start the *calendar* on local machine for development purposes.

## [calendar-backend](./calendar-backend.md)

#### Prerequisites

Before starting the backend, you will need to have the `rust` toolchain installed. 

Follow the instructions from [official site][rust-install-docs].

#### Start the backend

Clone the git repo
```Shell
git clone https://github.com/calendar-team/calendar-backend.git
```

`cd` into the directory
```Shell
cd calendar-backend
```

Start the app
```SHell
cargo run
```

## [calendar-frontend](./calendar-frontend.md)

#### Prerequisites

Before starting the frontend, you will need to have `Node.js` and `npm` installed.

Follow the instruction from [official site][nodejs-install-docs].

#### Start the frontend

Clone the git repo
```Shell
git clone https://github.com/calendar-team/calendar-frontend.git
```

`cd` into the directory
```Shell
cd calendar-frontend
```

Install locally all the dependencies from the project
```Shell
npm install
```

Start the app
```Shell
npm run dev
```

[rust-install-docs]: https://www.rust-lang.org/tools/install
[nodejs-install-docs]: https://nodejs.org/en
