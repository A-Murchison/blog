# goblog
Create a personal profile for yourself written in go


Your Repo (goblog)
│
├── posts/                  ← You write .md files here
│   ├── hello-world.md
│   └── my-go-journey.md
│
├── templates/              ← HTML templates (header, footer, layout)
│   └── layout.html
│
├── main.go                 ← Your Go CLI tool
│
└── public/                 ← GENERATED output (HTML files)
    ├── index.html
    ├── hello-world/
    │   └── index.html
    └── my-go-journey/
        └── index.html
