var SAMPLES = 200;
var SAMPLERATE = 1000; /* Hz */
var offset = 1024;
var MINvalue = 10000000;
var MAXvalue = 0;
var w = new Waveform(SAMPLES,{doubleBuffer:true, bits : 16});

LED.write(1);

w.on("buffer", function(buf) {

  g.clear();                      //draw bounding box
  g.drawRect(0, 0, 127, 63);
  g.moveTo(0,0);

  buf.forEach((y,x) => {
    g.lineTo(x,64-y/offset);      //draw graph lines

    if (y*3.6/65536 > MAXvalue) {            //check min/max
      MAXvalue = y*3.6/65536;
    }
    else if (y*3.6/65536 < MINvalue) {
      MINvalue = y*3.6/65536;
    }
  });

  g.setColor(0);                  //draw 
  g.fillRect(0,0,28,14);
  g.setColor(1);
  g.drawRect(0, 0, 28, 14);
  g.drawString("+" + (parseFloat(Math.round(MAXvalue * 100) / 100).toFixed(2)) + "V",3,2);
  g.drawString("-" + (parseFloat(Math.round(MINvalue * 100) / 100).toFixed(2)) + "V",3,8);

  g.flip();

  MINvalue = 65536;                //reset variables
  MAXvalue = 0;

});

w.startInput(A0,SAMPLERATE,{repeat:true});



setWatch(function() {              //setWatch for on board buttons
  w.stop();
  SAMPLERATE += 100;
  w.startInput(A0,SAMPLERATE,{repeat:true});
  console.log("Sample Rate = " + SAMPLERATE);
}, BTN1, {edge:"rising", debounce:50, repeat:true});

setWatch(function() {
  LED.write(1);
}, BTN2, {edge:"rising", debounce:50, repeat:true});

setWatch(function() {
  LED.write(0);
}, BTN3, {edge:"rising", debounce:50, repeat:true});

setWatch(function() {
  w.stop();
  SAMPLERATE -= 100;
  w.startInput(A0,SAMPLERATE,{repeat:true});
  console.log("Sample Rate = " + SAMPLERATE);
}, BTN4, {edge:"rising", debounce:50, repeat:true});


