---
title: Tweet activated rose
date: '2015-03-30'
category: craft-code
tags:
- arduino
- leds
- rose
- tweets
- wearables
- craft-code
status: published
---

<p>To see how to make the rose, please see my <a href="http://madebyrumyra.com/lighting-up-a-crochet-rose/">blog post over here on my craft blog</a>, (it seemed a more appropriate place for a <em>how to make</em> pattern).</p>

<p>TLDR; I crocheted a rose, a couple of rows of which contained wire, I then sewed LEDs on the rose in a parallel circuit. This post describes how I made it flash when someone tweets with a specified string, head down to the bottom of the post if you don't care about the code, there's a cool video :)</p>

<figure class="media-feature">
	<img src="media/featureCode.jpg" alt="Lit up crocheted rose, with equipment and code running to make it flash" />
	<figcaption></figcaption>
</figure>

<h3>The idea</h3>

<p>What I want to happen, now I have a rose which lights up, its to have it flash any time anyone tweets with a string I specify. (The idea came from my workplace, as O2 sponsor the England rugby team, the rose is the English rose and the hash tag to look out for was one O2 was promoting - #WearTheRose).</p>

<p>Along with the rose, I needed an <a href="http://arduino.cc/">Arduino</a> (I used an Arduino UNO), a script that looked for tweets containing the string I specified and broadcasted them to an Arduino script, which turned the LEDs on when triggered.</p>

READMORE

<h3>The code</h3>

<p>It took a lot of searching but most of the code came from one post, which due to the law of sods, I can not for the life of me find :( (I had it open for all the time - as soon as I find it I’ll update).</p>

<p>I had to make a few amendments. The first was adding in the Gemfile. (FYI I’m assuming you have ruby installed and are familiar with gems). For some reason it also wasn’t broadcasting the servo code, so I added line 33.</p>

<pre class="language-ruby"><code>require 'tweetstream'
require 'serialport'
 
input=ARGV.shift || "#bordeaux,#strasbourg"
#params for serial port
port_str = "/dev/tty.usbmodem1411"  #may be different for you
 
sp = SerialPort.new(port_str, 9600, 8, 1, SerialPort::NONE)
 
TweetStream.configure do |config|
  config.consumer_key       = 'CONSUMERKEYHERE'
  config.consumer_secret    = 'CONSUMERSECRETHERE'
  config.oauth_token        = 'OAUTHTOKENHERE'
  config.oauth_token_secret = 'OAUTHSECRETHERE'
  config.auth_method        = :oauth
end
 
@client=TweetStream::Client.new;
 
total=0
last=Time.now
words=input.split(',')
flags=Array.new(words.size)
buffers=words.map{|w| []}
sp.puts "512 0 0" # reset the servo
@client.track(words) do |tweet|
  p "beginning track of #{tweet.text}"
  begin
    search=tweet.text.downcase
    words.each_with_index do |word,i|
      if search.include? word
puts 'got something'
sp.puts "broadcasting tweet"
flags[i]=1
buffers[i]&lt;&lt;tweet
      end
    end
    if (Time.now-last)>0.11
      begin
ratio=(180*buffers[0].size/(buffers[0].size+buffers[1].size)).to_i
str=ratio.to_s+" "+flags.join(' ')
puts str
sp.puts str
last=Time.now
flags=Array.new(words.size,0)
      end
    end
  end
end
</code></pre>

<p>There’s a few things you have to set to make sure it runs. One is to create a Twitter app and add your own creds in where it specifies, the other is to make sure the USB port on line 6 is correct. Plug your Arduino in, and in the Arduino IDE go to <em>Tools &gt; Serial Port</em> and type what ever is next to the tick onto line. (E.g. “/dev/tty.usbmodem1411”).</p>

<p>If you navigate to the file in your terminal window and run ruby app.rb “stringtolookforhere” the tweets should start to be echoed out.</p>

<p>Next came the Arduino code, which seemed to work off the bat. I would recommend opening the <em>Serial Monitor</em> (again under <em>Tools</em> in the IDE) as you can visually see the broadcasts and when the lights should be on and off.</p>

<pre class="language-c"><code>int ledPin=13;    // select the input pin for the potentiometer
int nbLed=1;
 
void setup() {
  // Open serial communications and wait for port to open:
  Serial.begin(9600);
  while (!Serial) {
    ; // wait for serial port to connect. Needed for Leonardo only
  }
  for(int i=0;i&lt;nbLed;i++){
   pinMode(ledPin-i, OUTPUT); 
  }
}
 
// Utility function to get a value from a string at a given pos
String getValue(String data, char separator, int index)
{
  int found = 0;
  int strIndex[] = {0, -1};
  int maxIndex = data.length()-1;
 
  for(int i=0; i&lt;=maxIndex && found&lt;=index; i++){
    if(data.charAt(i)==separator || i==maxIndex){
found++;
strIndex[0] = strIndex[1]+1;
strIndex[1] = (i == maxIndex) ? i+1 : i;
    }
  }
  return found&gt;index ? data.substring(strIndex[0], strIndex[1]) : "";
}

void loop() {
  if(Serial.available() &gt;0) {
    String str=Serial.readStringUntil('\n');
    Serial.println("Read:"+str);
    for(int i=0;i&lt;nbLed;i++){
      // look for the next valid integer in the incoming serial stream:
      if(!getValue(str,' ',i+1).equals("0")){
digitalWrite(ledPin-i, HIGH);  
      }
    }
  }
  delay(100);  
  for(int i=0;i&lt;nbLed;i++){
    digitalWrite(ledPin-i, LOW); 
  } 
}</code></pre>

<h3>Hooking it all up</h3>

<p>All that’s left to do is upload the Arduino code to your Uno and attach the rose.</p>

<p>Attaching the rose was a very delicate operation, I’d already marked the positive and negative sides of the circuit, it was just a case of winding the wires carefully and making sure they didn’t touch and therefore short.</p>

<p>It did all manage to come together, however, even I was pretty amazed! Here's a video of the whole thing in action:</p>

<iframe width="560" height="315" style="border:2px solid grey; margin:20px auto;" src="https://www.youtube.com/embed/_MbP_Syy_mU?rel=0" frameborder="0" allowfullscreen></iframe>

<p>Looking forward I can not wait to take this idea further. There’s a Red Bear (bluetooth enabled Arduino) just sitting ready to try this with, which would make it much more portable (as long as I can find some power), as well as some much more fancy programmable LEDs.</p>

<p>Watch this space, I think there’s a lot more to come :)</p>
