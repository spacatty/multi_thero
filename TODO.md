## Landing

### Authentication

- [ ] Login
- [ ] Register
- [ ] Present?

Serverless structure w/
`OAUTH + EXPRESS + MONGO`

## Application

- UI:
  - [x] [Vuesax](https://vuesax.com/docs/components/)

### Layout

- [ ] Layout
  - [x] Navigation
  - [ ] Dark/Lght

---

### Audio module

iTunes Store API REQ e.g.

```
https://itunes.apple.com/search?term=seven+nation+army&entity=song&limit=1
```

#### Music

- [x] Card
- [ ] Full view
  - [ ] Meta

#### Podcasts

- [x] Card
- [ ] Full view
  - [ ] Meta

#### Audiobooks

- [x] Card
- [ ] Full view
  - [ ] Meta

---

### Video module

!Hookup themoviedb API (Cinema, series)
!Hook up YT API (Movies)

```
https://developers.themoviedb.org/3/tv-episodes/get-tv-episode-details
```

### Series

META

```
https://api.themoviedb.org/3/tv/84958?api_key=52217232f795bbefbb1b7c951aae98ad&language=ru-RU
```

CAST

```
https://api.themoviedb.org/3/tv/84958/credits?api_key=52217232f795bbefbb1b7c951aae98ad&language=ru-RU

```

- [x] Card
- [ ] Full view
  - [ ] Trailer player
  - [ ] Meta

#### Cinema

META

```
https://api.themoviedb.org/3/movie/497819?api_key=52217232f795bbefbb1b7c951aae98ad&language=ru-RU
```

CAST

```
https://api.themoviedb.org/3/movie/637649/credits?api_key=52217232f795bbefbb1b7c951aae98ad&language=en-EN
```

- [x] Card
- [ ] Full view
  - [ ] Trailer player
  - [ ] Meta

```
no cross-req required
```

#### Movies

- [x] Card
- [ ] Full view
  - [ ] YT-VIDEO
  - [ ] Meta
  - [ ] Recommendatioins?

---

# !!!

- [ ] State mgmt
- [ ] OAUTH + EXPRESS + MONGO
- [ ] Card line: fetch multiple pages
- [ ] FAVS
