# SQL-Island
<p>SQL Island is a fun introduction to learning and using SQL. The challenge can solved on this website <a href = "https://sql-island.informatik.uni-kl.de/">SQL ISLAND</a><br>This is my approach to solving the SQL Island challenge.</p>
 
 ## Question and Answer
 <b>QUESTION:</b> It seems there are a few people living in these villages. How can I see a list of all inhabitants?
 <p><strong>SELECT * <br>FROM INHABITANT;</strong></p>
 <b>QUESTION:</b> Man! I'm hungry. I will go and find a butcher to ask for some free sausages.
 <p><strong>SELECT * <br>FROM INHABITANT <br>WHERE job = 'butcher';</strong></p>
 <b>QUESTION:</b> Thank you, Edward! Okay, let's see who is friendly on this island...
 <p><strong>SELECT * <br>FROM INHABITANT <br>WHERE state = 'friendly';</strong></p>
 <b>QUESTION:</b> There is no way around getting a sword for myself. I will now try to find a friendly weaponsmith to forge me one.
 <p><strong>SELECT *<br>FROM INHABITANT<br>WHERE state = 'friendly' AND job = 'weaponsmith';</strong></p>
 <b>QUESTION:</b> Oh, that does not look good. Maybe other friendly smiths can help you out, e.g. a blacksmith. Try out: job LIKE '%smith' to find all inhabitants whose job ends with 'smith'. 
 <p><strong>SELECT * <br>FROM INHABITANT <br>WHERE state = 'friendly' AND job LIKE '%smith';</strong></p>
 <b>QUESTION:</b> That looks better! I will go and visit those smiths. Hi stranger! Where are you going? I'm Paul, I'm the major of Monkeycity. I will go ahead and register you as a citizen.
 <p><strong>INSERT INTO INHABITANT (name, villageid, gender, job, gold, state) <br>VALUES ('Stranger', 1, '?', '?', 0, '?');</strong></p>
 <b>QUESTION:</b> No need to call me stranger! What's my personid? 
 <p><strong>SELECT personid <br>FROM INHABITANT<br>WHERE name = 'Stranger';</strong></p>
 <p><i>NOTE: This returns a personid of 20</i><br></p>
 <b>QUESTION:</b> Hi Ernest! How much is a sword? I can offer to make you a sword for 150 gold. That's the cheapest you will find! How much gold do you have?
 <p><strong>SELECT gold<br>FROM INHABITANT<br>WHERE personid = 20;</strong></p>
 <b>QUESTION:</b> Damn! No mon, no fun. There has to be another option to earn gold other than going to work. Maybe I could collect ownerless items and sell them! Can I make a list of all items that don't belong to anyone?
 <p><strong>SELECT *<br>FROM ITEM<br>WHERE owner ISNULL;</strong></p>
 <b>QUESTION:</b> So much cool stuff! Yay, a coffee cup. Let's collect it!
 <p><strong>UPDATE ITEM <br>SET owner = 20 <br>WHERE item = 'coffee cup';</strong></p>
 <b>QUESTION:</b> Do you know a trick how to collect all the ownerless items?
 <p><strong>UPDATE ITEM<br>SET owner = 20<br>WHERE owner ISNULL;</strong></p>
 <b>QUESTION:</b> Now list all of the items I have!
 <p><strong>SELECT *<br>FROM ITEM<br>WHERE owner = 20;</strong></p>
 <b>QUESTION:</b> Find a friendly inhabitant who is either a dealer or a merchant. Maybe they want to buy some of my items.
 <p><strong>SELECT *<br>FROM INHABITANT<br>WHERE state = 'friendly' <br>AND job = 'dealer' OR job = 'merchant';</strong></p>
 <b>QUESTION:</b> I'd like to get the ring and the teapot. The rest is nothing but scrap. Please give me the two items. My personid is 15.
 <p><strong>UPDATE ITEM<br>SET owner = 15<br>WHERE item IN ('teapot', 'ring');</strong></p>
 <b>QUESTION:</b> Thank you! Here, some gold!
 <p><strong>UPDATE INHABITANT <br>SET gold = gold + 120 <br>WHERE personid = 20;</strong></p>
 <b>QUESTION:</b> Unfortunately, that's not enough gold to buy a sword. Seems like I do have to work after all. Maybe it's not a bad idea to change my name from Stranger to my real name before I will apply for a job.
 <p><strong>UPDATE INHABITANT<br>SET name = Ahmed<br>WHERE name = 'Stranger';</strong></p>
 <b>QUESTION:</b> Since baking is one of my hobbies, why not find a baker who I can work for? 
 <p><strong>SELECT *<br>FROM INHABITANT<br>WHERE job = 'baker'<br>ORDER BY gold DESC;</strong></p>
 <p> Aha, Paul! I know him!
Hi, you again! So, Ahmed Ayodele is your name. I saw you want to work as a baker? Okay! You will be paid 1 gold for 100 bread rolls.
(8 hours later...) Here, I made ten thousand bread rolls! I quit! This should be enough money to buy a sword. Let's see what happens with my gold balance.
Here's your new sword, Ahmod Ayodolo! Now you can go everywhere.
My name is Ahmed Ayodele! Thanks anyway!</p>
 <b>QUESTION:</b> Is there a pilot on this island by any chance? He could fly me home. 
 <p><strong>SELECT *<br>FROM INHABITANT<br>WHERE job = 'pilot';</strong></p>
 <table style="border: thin solid coral">
  <thead>
    <td>personid</td>
    <td>name</td>
    <td>villageid</td>
    <td>gender</td>
    <td>job</td>
    <td>gold</td>
    <td>state</td>
  </thead>
  <tr>
    <td>8</td>
    <td>Arthur Tailor</td>
    <td>2</td>
    <td>m</td>
    <td>pilot</td>
    <td>490</td>
    <td>kidnapped</td>
  </tr>
 </table>
 <p>Oh no, his state is 'kidnapped'. Horrible, the pilot is held captive by Dirty Dieter!</p>
 <b>QUESTION:</b> I will show you a trick how to find out the name of the village where Dirty Dieter lives.
 <p><strong>SELECT village.name <br>FROM VILLAGE, INHABITANT <br>WHERE village.villageid = inhabitant.villageid <br>AND inhabitant.name = 'Dirty Dieter';</strong></p>
 <p><i>NOTE: This returns the village name as 'Onionville'.</i><br></p>
 <b>QUESTION:</b> Find out the chief's name of the village Onionville? 
 <p><strong>SELECT inhabitant.name<br>FROM VILLAGE, INHABITANT<br>ON village.villageid = inhabitant.villageid<br>WHERE village.name = 'Onionville' <br>AND village.chief = inhabitant.personid;
</strong></p>
<p>This returns the inhabitant name as Fred Dix</p>
<p>I've got it! I will visit Fred and ask him about Dirty Dieter and the pilot.</p>
<b>QUESTION:</b> Um, how many inhabitants does Onionville have?
<p><strong>SELECT COUNT(*) <br>FROM INHABITANT, VILLAGE <br>WHERE village.villageid = inhabitant.villageid <br>AND village.name = 'Onionville';</strong></p>
<p>This returns a total count of 8</p>
<b>QUESTION:</b> Hello Ahmed, the pilot is held captive by Dirty Dieter in his sister's house. Shall I tell you how many women there are in Onionville? Nah, you can figure it out by yourself!
<p><strong>SELECT COUNT(*)<br>FROM VILLAGE, INHABITANT<br>ON village.villageid = inhabitant.villageid<br>WHERE village.name = 'Onionville' <br>AND inhabitant.gender = 'f';</strong></p>
<p>This returns a total count of 1</p>
<b>QUESTION:</b> Oh, only one woman. What's her name?
<p><strong>SELECT inhabitant.name<br>FROM VILLAGE, INHABITANT<br>ON village.villageid = inhabitant.villageid<br>WHERE village.name = 'Onionville' <br>AND inhabitant.gender = 'f';</strong></p>
<p>This returns the name: Dirty Diane</p>
<p>Let's go!</p>
<b>QUESTION:</b> Ahmed, if you hand me over the entire property of our nearby village Cucumbertown, I will release the pilot. I will show you now what this property consists of.
<p><strong>SELECT SUM(inhabitant.gold) <br>FROM INHABITANT, VILLAGE <br>WHERE village.villageid = inhabitant.villageid <br>AND village.name = 'Cucumbertown';</strong></p>
This return the sum of inhabitant gold to be 8980.
<b>QUESTION:</b> Oh no, baking bread alone can't solve my problems. If I continue working and selling items though, 
I could earn more gold than the worth of gold inventories of all bakers, dealers and merchants together. How much gold is that?
<p><strong>SELECT SUM(gold)<br>FROM INHABITANT<br>WHERE job = 'baker' <br>OR job = 'dealer' <br>OR job = 'merchant';</strong></p>
This return the sum of gold to be 4130.
<p>That's not enough.</p>
<b>QUESTION:</b> Let's have a look at how much average gold people own, depending on their job.
<p><strong>SELECT job, SUM(inhabitant.gold), AVG(inhabitant.gold) <br>FROM inhabitant <br>GROUP BY job <br>ORDER BY AVG(inhabitant.gold);</strong></p>
<table style="border: thin solid coral">
  <thead>
    <td>job</td>
    <td>SUM(inhabitant.gold)</td>
    <td>AVG(inhabitant.gold)</td>
  </thead>
  <tr>
    <td>farmer</td>
    <td>10</td>
    <td>10</td>
  </tr>
  <tr>
    <td>?</td>
    <td>70</td>
    <td>70</td>
  </tr>
  <tr>
    <td>merchant</td>
    <td>250</td>
    <td>250</td>
  </tr>
  <tr>
    <td>blacksmith</td>
    <td>390</td>
    <td>390</td>
  </tr>
  <tr>
    <td>weaponsmith</td>
    <td>790</td>
    <td>395</td>
  </tr>
  <tr>
    <td>author</td>
    <td>420</td>
    <td>420</td>
  </tr>
  <tr>
    <td>pilot</td>
    <td>490</td>
    <td>490</td>
  </tr>
  <tr>
    <td>baker</td>
    <td>1750</td>
    <td>583.333333333333</td>
  </tr>
  <tr>
    <td>smith</td>
    <td>1250</td>
    <td>625</td>
  </tr>
  <tr>
    <td>dealer</td>
    <td>2130</td>
    <td>710</td>
  </tr>
  <tr>
    <td>butcher</td>
    <td>11370</td>
    <td>2842.5</td>
  </tr>
</table>
<b>QUESTION:</b> Very interesting: For some reason, butchers own the most gold. How much gold do different inhabitants have on average, depending on their state (friendly, ...)?
<p><strong>SELECT state, avg(gold)<br>FROM INHABITANT<br>GROUP BY state;</strong></p>
<table style="border: thin solid coral">
  <thead>
        <td>job</td>
        <td>avg(gold)</td>
  </thead>
  <tr>
    <td>?</td>
    <td>70</td>
  </tr>
  <tr>
    <td>evil</td>
    <td>512.85714285714</td>
  </tr>
  <tr>
    <td>friendly</td>
    <td>706.363636363636</td>
  </tr>
  <tr>
    <td>kidnapped</td>
    <td>490</td>
  </tr>
</table>
<b>QUESTION:</b> Ok, so the only way is to mug the villains. Or I might as well go ahead and just kill Dirty Dieter with my sword!
<p><strong>DELETE FROM INHABITANT <br>WHERE name = 'Dirty Dieter';</strong></p>
<b>QUESTION:</b> Heeeey! Now I'm very angry! What will you do next, Ahmed?
<p><strong>DELETE FROM INHABITANT<br>WHERE name = 'Dirty Diane';</strong></p>
<b>QUESTION:</b> Yeah! Now I release the pilot!
<p><strong>UPDATE INHABITANT<br>SET state = 'friendly'<br>WHERE job = 'pilot';</strong></p>
<p>Thank's for releasing me, Ahmed! I will fly you home!</p>
<b>QUESTION:</b> I take my sword, some gold and lots of useless items with me as a souvenir. What a big adventure!
<p><strong>UPDATE INHABITANT <br>SET state = 'emigrated' <br>WHERE personid = 20;</strong></p>
