<!doctype html>
<html>
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no"/>
  <title>Goal Game</title>
  <style>
    html,body{height:100%;margin:0;background:#0b1f2a;overflow:hidden}
    #game{width:100vw;height:100vh}
    canvas,body{touch-action:none}
  </style>
  <script src="https://cdn.jsdelivr.net/npm/phaser@3.70.0/dist/phaser.min.js"></script>
</head>
<body>
<div id="game"></div>
<script>
class MainScene extends Phaser.Scene{
  constructor(){super('main')} 
  init(){
    this.players=[];this.playerIndex=0;this.passCount=0;this.multiplier=1;this.missChance=.05;this.inFlight=false;this.gameOver=false;this.countdownEvent=null;this.countdownText=null;this.countdownRemaining=0;this.firstPassDone=false;
  }
  create(){
    this.W=540;this.H=960;this.PLAYERS_COUNT=10;this.P_SPACING_MIN=420;this.H_OFFSET=140;this.BALL_R=20;this.PW=64;this.PH=96;this.PASS_MIN=2000;this.PASS_RAND=1000;this.MS_STEP=.07;this.ML_STEP=.20;this.BAR_MAX=10;
    const btnH=64,btnCY=this.H-70,bottomMargin=this.H-(btnCY+btnH/2),firstCenterY=btnCY-btnH/2-bottomMargin-this.PH/2;
    const cx=this.W/2,marginX=this.PW/2+10;this.positions=[];let y=firstCenterY;
    for(let i=0;i<this.PLAYERS_COUNT;i++){const x=i===0?cx:Phaser.Math.Clamp(cx+Phaser.Math.Between(-this.H_OFFSET,this.H_OFFSET),marginX,this.W-marginX);if(i>0)y-=this.P_SPACING_MIN+Phaser.Math.Between(0,this.P_SPACING_MIN);this.positions.push({x,y})}
    const minY=this.positions.reduce((m,p)=>Math.min(m,p.y),this.positions[0].y);const top=minY-700,bottom=this.H+500,worldH=bottom-top;this.cameras.main.setBounds(0,top,this.W,worldH);this.physics.world.setBounds(0,top,this.W,worldH);
    this.add.rectangle(this.W/2,(top+bottom)/2,this.W,worldH,0x228B22).setDepth(-10);for(let sy=top;sy<bottom;sy+=160){this.add.rectangle(this.W/2,sy+80,this.W,2,0x1a5e1a).setDepth(-9)}
    for(let i=0;i<this.PLAYERS_COUNT;i++){const pos=this.positions[i];const b=this.makePlayer(pos.x,pos.y);this.players.push({body:b})}
    const last=this.players[this.PLAYERS_COUNT-1].body;this.goal=this.add.rectangle(this.W/2,last.y-260,110,26,0x2fd39f).setStrokeStyle(4,0x1aa67a).setDepth(9);this.add.text(this.goal.x,this.goal.y-36,'GOAL',{fontFamily:'monospace',fontSize:18,color:'#7fffd4'}).setOrigin(.5).setDepth(9);
    const first=this.players[0].body;const leg=this.legPos(first);this.ball=this.add.circle(leg.x,leg.y,this.BALL_R,0xffffff).setDepth(100);this.cameras.main.startFollow(this.ball,true,.22,.22);
    this.barBG=this.add.rectangle(28,this.H/2,18,760,0x103047).setOrigin(.5).setDepth(50).setScrollFactor(0);this.barFG = this.add.rectangle(28, this.H/2+380, 12, 760, 0x34c3ff).setOrigin(.5,1).setDepth(51).setScrollFactor(0);
    this.barFG.setScale(1, 0);this.multText=this.add.text(56,24,'x1',{fontFamily:'monospace',fontSize:22,color:'#b9eeff'}).setScrollFactor(0).setDepth(51);this.missText=this.add.text(56,56,'Miss: 5%',{fontFamily:'monospace',fontSize:16,color:'#ffb3b3'}).setScrollFactor(0).setDepth(51);
    this.ui=this.add.container(0,0).setScrollFactor(0).setDepth(2000);const by=btnCY;this.passBtn=this.mkBtn('START',this.W/2,by,220,64,0x3ddc97,()=>this.startFirstPass());this.catchBtn=this.mkBtn('CATCH!',this.W/2,by,220,64,0xf7b267,()=>this.catch());this.setBtn(this.passBtn,true);this.setBtn(this.catchBtn,false);this.ui.add([this.passBtn,this.catchBtn]);
    this.overlay=this.add.container(0,0).setScrollFactor(0).setDepth(3000).setVisible(false);const dim=this.add.rectangle(this.W/2,this.H/2,this.W,this.H,0x000,0.5);dim.setInteractive();this.ovTitle=this.add.text(this.W/2,this.H/2-70,'',{fontFamily:'monospace',fontSize:36,color:'#fff'}).setOrigin(.5);this.ovMsg=this.add.text(this.W/2,this.H/2-16,'',{fontFamily:'monospace',fontSize:20,color:'#dff6ff'}).setOrigin(.5);this.restartBtn=this.mkBtn('RESTART',this.W/2,this.H/2+56,220,64,0x49dceb,()=>this.restart());this.overlay.add([dim,this.ovTitle,this.ovMsg,this.restartBtn]);
    this.hud();
  }
  makePlayer(x,y){
    const skin=0xffd2a6, shirt=0xff3b30, hair=0x111111, part=this.PH/5;
    const c=this.add.container(x,y).setDepth(10);
    const seg=(color,start,count)=>{const h=part*count, cy=-this.PH/2+part*(start+count/2); c.add(this.add.rectangle(0,cy,this.PW,h,color).setOrigin(0.5));};
    seg(hair,0,1);
    seg(skin,1,1);
    seg(shirt,2,1);
    seg(shirt,3,1);
    seg(skin,4,1);
    return c;
  }
  mkBtn(t,x,y,w,h,c,cb){const b=this.add.container(x,y).setDepth(200).setScrollFactor(0);const bg=this.add.rectangle(0,0,w,h,c).setOrigin(.5);const tx=this.add.text(0,0,t,{fontFamily:'monospace',fontSize:26,color:'#072c2c'}).setOrigin(.5);const z=this.add.zone(0,0,w,h).setOrigin(.5).setScrollFactor(0).setInteractive({useHandCursor:true});z.on('pointerdown',()=>{if(this.gameOver&&b!==this.restartBtn)return;if(this.inFlight&&b!==this.restartBtn)return;cb()});b.add([bg,tx,z]);b.hitZone=z;return b}
  setBtn(b,a){b.setVisible(a);if(b.hitZone){a?b.hitZone.setInteractive({useHandCursor:true}):b.hitZone.disableInteractive()}}
  legPos(p){return{x:p.x,y:p.y+this.PH/2-this.BALL_R*.5-2}}
  getPassT(){return this.PASS_MIN+Phaser.Math.Between(0,this.PASS_RAND)}
  startFirstPass(){if(this.firstPassDone)return;this.setBtn(this.passBtn,false);this.setBtn(this.catchBtn,true);this.pass()}
  startCountdown(){if(!this.firstPassDone||this.gameOver)return;this.cancelCountdown();this.countdownRemaining=1;const h=this.players[this.playerIndex].body;this.countdownText=this.add.text(h.x,h.y-this.PH/2-56,String(this.countdownRemaining),{fontFamily:'monospace',fontSize:40,color:'#ffe28b'}).setOrigin(.5).setDepth(200).setAlpha(0);this.countdownEvent=this.time.addEvent({delay:500,callback:()=>{if(this.gameOver||this.inFlight)return;this.cancelCountdown();this.pass()}})}
  cancelCountdown(){if(this.countdownEvent){this.countdownEvent.remove(false);this.countdownEvent=null}if(this.countdownText){this.countdownText.destroy();this.countdownText=null}}
  pass(){if(this.playerIndex>=this.PLAYERS_COUNT-1){this.toGoal();return}this.toPlayer(this.playerIndex+1)}
  arcTo(tx,ty,d,cb){const s=new Phaser.Math.Vector2(this.ball.x,this.ball.y),e=new Phaser.Math.Vector2(tx,ty),m=s.clone().add(e).scale(.5),tr=e.distance(s),arc=Math.max(220,Phaser.Math.Clamp(tr*.35,180,380)),c=new Phaser.Math.Vector2(m.x,m.y-arc),curve=new Phaser.Curves.QuadraticBezier(s,c,e);return this.tweens.addCounter({from:0,to:1,duration:d,ease:'Sine.easeInOut',onUpdate:tw=>{const t=tw.getValue(),p=curve.getPoint(t);this.ball.setPosition(p.x,p.y);const scale=1+.5*Math.sin(Math.PI*t);this.ball.setScale(scale,scale)},onComplete:cb})}
  toPlayer(i){const miss=Math.random()<this.missChance,t=this.players[i].body;this.inFlight=true;const leg=this.legPos(t),dur=this.getPassT();if(miss){const mx=Phaser.Math.Linear(this.ball.x,leg.x,.6)+Phaser.Math.Between(-80,80),my=leg.y-80;this.arcTo(mx,my,dur,()=>this.fail());this.cameras.main.shake(300,.003)}else{this.arcTo(leg.x,leg.y,dur,()=>{this.playerIndex=i;this.passCount++;this.multiplier+=1;this.missChance+=this.MS_STEP;this.inFlight=false;this.cameras.main.shake(300,.003);this.showMultiplierPop(t.x,t.y-this.PH/2-24);if(!this.firstPassDone)this.firstPassDone=true;this.hud();this.startCountdown()})}}
  toGoal(){const miss=Math.random()<this.missChance;this.inFlight=true;const dur=this.getPassT();if(miss){const mx=this.goal.x+Phaser.Math.Between(-120,120),my=this.goal.y-140;this.arcTo(mx,my,dur,()=>this.fail());this.cameras.main.shake(300,.003)}else{this.arcTo(this.goal.x,this.goal.y+6,dur,()=>{this.passCount++;this.multiplier+=1;this.missChance+=this.MS_STEP;this.inFlight=false;this.hud();this.startCountdown()})}}
  showMultiplierPop(x,y){const txt=this.add.text(x,y,'x'+this.multiplier.toFixed(0),{fontFamily:'monospace',fontSize:48,color:'#ffffff',stroke:'#103047',strokeThickness:6}).setOrigin(.5).setDepth(2000);txt.setScale(.1,.1);this.tweens.add({targets:txt,scaleX:1.15,scaleY:1.15,y:y-10,duration:220,ease:'Back.Out'});this.tweens.add({targets:txt,scaleX:1,scaleY:1,delay:220,duration:140,ease:'Sine.easeOut'});this.time.delayedCall(900,()=>txt.destroy())}
  catch(){if(this.inFlight||this.gameOver)return;this.cancelCountdown();const r=Math.round(100*this.multiplier);this.ovMsg.setText('Multiplier: x'+this.multiplier.toFixed(0)+'\nReward: '+r);this.ovTitle.setText('YOU WIN! ✨');this.overlay.setVisible(true);this.overlay.setAlpha(0);this.tweens.add({targets:this.overlay,alpha:1,duration:250});this.gameOver=true}
  fail(){this.cancelCountdown();this.inFlight=false;this.gameOver=true;this.tweens.add({targets:this.ball,scaleX:1.5,scaleY:1.5,yoyo:true,repeat:1,duration:160});this.ovMsg.setText('No reward this time.');this.ovTitle.setText('MISSED! ❌');this.overlay.setVisible(true);this.overlay.setAlpha(0);this.tweens.add({targets:this.overlay,alpha:1,duration:250})}
  hud(){
    const progress = Phaser.Math.Clamp((this.multiplier - 1) / (this.BAR_MAX - 1), 0, 1);
    this.barFG.setScale(1, progress);
    this.multText.setText('x' + this.multiplier.toFixed(0));
    this.missText.setText('Miss: ' + (this.missChance * 100).toFixed(0) + '%');
  }
  restart(){this.cancelCountdown();this.gameOver=false;this.inFlight=false;this.firstPassDone=false;this.playerIndex=0;this.passCount=0;this.multiplier=1;this.missChance=.05;this.overlay.setVisible(false);const f=this.players[0].body,l=this.legPos(f);this.ball.setPosition(l.x,l.y);this.ball.setScale(1,1);this.cameras.main.startFollow(this.ball,true,.22,.22);this.cameras.main.pan(this.ball.x,this.ball.y,0);this.setBtn(this.passBtn,true);this.setBtn(this.catchBtn,false);this.hud()}
}
new Phaser.Game({type:Phaser.AUTO,parent:'game',backgroundColor:'#0b1f2a',physics:{default:'arcade',arcade:{debug:false}},scale:{mode:Phaser.Scale.FIT,autoCenter:Phaser.Scale.CENTER_BOTH,width:540,height:960},scene:[MainScene]});
</script>
</body>
</html>
