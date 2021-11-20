## Форма поиска ✅

- [x] Форма изначально есть в HTML документе.
- [x] Пользователь будет вводить строку для поиска в текстовое поле,
- [x] а при сабмите формы необходимо выполнять HTTP-запрос.

## HTTP-запросы ✅

- [x] В качестве бэкенда используй публичный API сервиса Pixabay.
- [x] Зарегистрируйся, получи свой уникальный ключ доступа и ознакомься с
      документацией.
- [x] Список параметров строки запроса, указать `обязательно`:
  - [x] `key` - твой уникальный ключ доступа к API.
  - [x] `q` - термин для поиска. `Ввод пользователя`.
  - [x] `image_type` - тип изображения. Мы хотим `photo`.
  - [x] `orientation` - ориентация фотографии. Задай значение `horizontal`.
  - [x] `safesearch` - фильтр по возрасту. Задай значение `true`.

### Ответ сервера ✅

В нем будет массив изображений удовлетворивших критериям параметров запроса.
Каждое изображение описывается объектом, из которого тебе интересны только
следующие свойства:

- [x] `webformatURL` - ссылка на маленькое изображение для списка карточек.
- [x] `largeImageURL` - ссылка на большое изображение.
- [x] `tags` - строка с описанием изображения. Подойдет для атрибута alt.
- [x] `likes` - количество лайков.
- [x] `views`- количество просмотров.
- [x] `comments` - количество комментариев.
- [x] `downloads` - количество загрузок.

### Если пустой массив ✅

- [x] Если бэкенд возвращает пустой массив, значит ничего подходящего найдено
      небыло. В таком случае показывай уведомление с текстом
      `"Sorry, there are no images matching your search query. Please try again."`.
      Для уведомлений используй библиотеку notiflix.

## Галерея и карточка изображения ✅

- [x] Элемент `div.gallery` изначально есть в HTML документе, и в него
      необходимо рендерить разметку карточек изображений.
- [x] При поиске по новому ключевому слову необходимо полностью очищать
      содержимое галереи, чтобы не смешивать результаты.

```html
<div class="gallery"><!-- Карточки изображений --></div>
```

### Шаблон разметки карточки одного изображения для галереи. ✅

```html
<div class="photo-card">
  <img src="" alt="" loading="lazy" />
  <div class="info">
    <p class="info-item"><b>Likes</b></p>
    <p class="info-item"><b>Views</b></p>
    <p class="info-item"><b>Comments</b></p>
    <p class="info-item"><b>Downloads</b></p>
  </div>
</div>
```

## Пагинация ✅

- [x] Pixabay API поддерживает пагинацию и предоставляет параметры `page` и
      `per_page`. Сделай так, чтобы в каждом ответе приходило `40` объектов (по
      умолчанию 20).
- [x] Изначально значение параметра `page` должно быть `1`.
- [x] `При каждом последующем запросе`, `page` необходимо увеличить на `1`.
- [x] `При поиске по новому ключевому слову` значение `page` надо
      `вернуть в исходное`, для пагинации по новой коллекции изображений.

- [x] В HTML документе уже есть разметка кнопки `Load more`.
  ```html
  <button type="button" class="load-more">Load more</button>
  ```
  - [x] При клике по которой необходимо:
    - [x] выполнять запрос за следующей группой изображений
    - [x] и добавлять разметку к уже существующим элементам галереи.
- [x] Изначально кнопка должна быть скрыта.
- [x] После первого запроса кнопка появляется в интерфейсе под галереей.

- [x] При повторном сабмите кнопка прячется, а после запроса опять отображается.
- [x] В ответе бэкенд возвращает свойство `totalHits` - общее количество
      изображений которые подошли под критерий поиска (для бесплатного
      аккаунта).
- [x] Если пользователь дошел до конца коллекции, прячь кнопку и выводи
      уведомление с текстом
      `"We're sorry, but you've reached the end of search results."`.
- [x] После первого запроса при каждом новом поиске выводить уведомление в
      котором будет написано сколько всего нашли изображений (свойство
      totalHits). Текст уведомления `"Hooray! We found totalHits images."`

### Библиотека SimpleLightbox ✅

Добавить отображение большой версии изображения с библиотекой SimpleLightbox для
полноценной галереи.

- [x] В разметке необходимо будет обернуть каждую карточку изображения в ссылку,
      как указано в документации.
- [x] У библиотеки есть метод `refresh()` который обязательно нужно вызывать
      каждый раз после добавления новой группы карточек изображений.
- [x] Для того чтобы подключить CSS код библиотеки в проект, необходимо добавить
      еще один импорт, кроме того который описан в документации.

```js
// Описан в документации
import SimpleLightbox from 'simplelightbox';
// Дополнительный импорт стилей
import 'simplelightbox/dist/simple-lightbox.min.css';
```

### Прокрутка страницы ✅

- [x] Сделать плавную прокрутку страницы после запроса и отрисовки каждой
      следующей группы изображений. Вот тебе код подсказка, а разберись в нём
      самостоятельно.

```js
const { height: cardHeight } = document
  .querySelector('.gallery__list')
  .firstElementChild.getBoundingClientRect();

window.scrollBy({
  top: cardHeight * 2,
  behavior: 'smooth',
});
```

### Бесконечный скролл

- [ ] Вместо кнопки «Load more» можно сделать бесконечную загрузку изображений
      при прокрутке страницы. Мы предоставлям тебе полную свободу действий в
      реализации, можешь использовать любые библиотеки.

UI/UX test cases:

- random query - `Sorry no images`
- cat - `Horray 500 images` + `init simpleLightbox`
- dog - `Horray 500 images` + `reinit simpleLightbox`
- random query - `markup is empty`
