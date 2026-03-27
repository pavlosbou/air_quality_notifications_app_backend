# ENVIRONMENTAL DATA VISUALIZATION AND ANALYSIS SYSTEM

## Bachelor thesis

### Harokopeio University of Athens

<p> In this repository you can find the implementation of the backend part of my thesis.</p>

<p>To create it I used the following technologies:</p>

<ul>
  <li>Node-red</li>
  <li>Sqlite</li>
  <li>Firebase Real Time Database</li>
  <li>RabbitMQ</li>
  <li>WebSockets</li>
</ul>

<p>The environmental data I use are metrics of air polution such us nanoparticles that exist in the air. <br/>
   To create the dataset, I call the weather api two times a day, every 12 hours, for every capital city in europe and save the response in the database.<br/>
   When the dataset is ready and after then once a day, I use the K means algorithm to extract three clusters with data so2, pm2_5 and pm10 in relation with the wind<br/>
   </p>

<p>To create the notifications, I call the api every 3 hours and I compare the response's wind speed with the centroid's value and then I categorize the notification in three categories:0
  <ul>
    <li>good quality for big values</li> 
    <li>not bad but be careful quality for values close to the centroid</li>
    <li>bad quality. for small values</ul></p>
<p>
  Then I batch the notifications and save them in the Firebase realtime database. When the response from the real time databse comes, the notifications get published in a topic exchange in RabbitMQ. The topic is the city's name. In the frontend the user chooses in which cities wants to subscribe and a binding to each city's qeue is created and the user is able to consume the notifications.
</p>

<p>Also an extra layer, webSockets, has been created and at the end the user can view the notifications.</p>

<p> The user authentication is custom and I created it inside node-red and I handled it with the use of jwt tokens. The password gets hashed before it gets stored in the database. </p>
