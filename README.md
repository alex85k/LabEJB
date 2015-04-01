== Практика по EJB - продолжение ==

 1. Откройте проект из прошлой практики https://netbeans.org/kb/docs/javaee/javaee-entapp-ejb_ru.html
 2. Вместо компонентов, работающих с очередью JMS, используйте обычные сеансовые компоненты:
      - Вызывайте компонент NewsEntityFacade из сервлета напрямую, без отправления сообщения (createSession, createProducer, send) и приёма его компонентом NewMessage (@EJB NewsEntityFacade facade в сервлете)
 3. Перенесите HTML-содержимое из обоих сервлетов в новые jsp-страницы list.jsp и post.jsp в папке WEB-INF
      - из сервлета вызывайте переход на эти страницы операторами типа
      
      ```
       request.getRequestDispatcher("/WEB-INF/post.jsp").forward(request, response);
      ```
      - в сервлете ListNews перед передачей управления на list.jsp сохраните в атрибутах запроса нужные для показа данные      
      ```
      newsEntityFacade.findAll() sessionManagerBean.getActiveSessionsCount()
      ```
      
      - печать списка сообщений реализуйте с помощью тегов JSTL типа 
      
      ```
      <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
      ...
        <c:forEach items="${msgs}" var="msg">
            <c:out value="${msg.body}"/> <br/>
            ....
        </c:forEach>
      ```
  4. Добавьте редактирование сообщений
      - по запросу /EditMessage?id=7 выводите форму редактирования заданного сообщения (сервлет получает данные из БД и передаёт управление edit.jsp
      - edit.jsp по кнопке "сохранить" выполняет запрос на адрес, которму назначено действие сохранения (отдельный сервлет, вносящий изменение в базу с помощью фасада)

  
