//-------------------------------------------------
// Anti-Radiation Boots
//-------------------------------------------------

const STRIP_RADBOOTS=1500;
const ENC_RADBOOTS=35;
const HDLD_RADBOOTS="RDB";//RaD Boots, lol

class WornRadBoots:HDDamageHandler{
	default{
		+nointeraction;
		+noblockmap;
		-hdpickup.fullcoverage
		//this flag controls whether you can bandage 
		//with it equipped or not
	
		-inventory.isarmor
		inventory.maxamount 1;inventory.amount 1;
		HDDamageHandler.priority 1000;
		HDPickup.wornlayer STRIP_RADBOOTS;
		HDPickup.overlaypriority 150;
		tag "anti-radiation boots";
	}
	states{spawn:TNT1 A 0;stop;}
	override inventory createtossable(int amt){
		let rrr=owner.findinventory("ProtectiveRadBoots");
		if(rrr)owner.useinventory(rrr);else destroy();
		return null;
	}
	override void attachtoowner(actor owner){
		if(!owner.countinv("ProtectiveRadBoots"))
			owner.A_GiveInventory("ProtectiveRadBoots");
			
		super.attachtoowner(owner);
	}
	override void DetachFromOwner(){
		owner.A_TakeInventory("ProtectiveRadBoots",1);
		HDArmour.ArmourChangeEffect(owner,60);
		//this triggers the stun effect when removing gear
		//the number seems to control how long the stun lasts
		
		super.DetachFromOwner();
	}
	override void DoEffect(){
	//stuff here happens every tic
		if(stamina>0)stamina--;
	}
	override double RestrictSpeed(double speedcap){
	//this changes how fast a player can move while wearing this
		return min(speedcap, 1.6);//default is 1.8
	}//lower speedcap since rad boots are thicker and more durable,	
	 //but a bit heavy to walk in compared to a radsuit
	 
/* this is where the radsuit's visor overlay is handled,
	can be useful for adding certain visual effects


	override void DisplayOverlay(hdstatusbar sb,hdplayerpawn hpl){
		sb.SetSize(0,320,200);
		sb.BeginHUD(forcescaled:true);
		sb.fill(
			color(sb.blurred?(level.time&(1|2|4))<<2:160,10,40,14),
			0,0,screen.getwidth(),screen.getheight()
		);
	}
*/
	//screw it, going back to the old DrawHUDStuff code,
	//i'm not dealing with stupid statusbar bullshit
	override void DrawHudStuff(
		hdstatusbar sb,
		hdplayerpawn hpl,
		int hdflags,
		int gzflags
	){
		bool am=hdflags&HDSB_AUTOMAP;
		sb.drawimage(
			"RDBTA0",
			am?(11,137):(84,-3),
			am?sb.DI_TOPLEFT:
			(sb.DI_SCREEN_CENTER_BOTTOM|sb.DI_ITEM_CENTER_BOTTOM)
		);
	}


//this is where you can change how equipment affects the
//way players receive damage when wearing it, here it
//negates all damges caused by slime floors

	//called from HDPlayerPawn and HDMobBase's DamageMobj
	override int,name,int,double,int,int,int HandleDamage(
		int damage,
		name mod,
		int flags,
		actor inflictor,
		actor source,
		double towound,
		int toburn,
		int tostun,
		int tobreak
	){
		let victim=owner;
		if(
			(flags&DMG_NO_ARMOR)
			||mod=="maxhpdrain"
			||mod=="internal"
			||mod=="jointlock"
			||mod=="bleedout"
			||!victim
		)return damage,mod,flags,towound,toburn,tostun,tobreak;

		bool breached=false;

		if(mod=="slime"){	//this is literally the only thing these boots protect against
			victim.A_SetInventory("Heat",countinv("Heat")+max(0,damage-random(4,20)));
			damage=0;
			//need to add a check here to ignore protectiom if incapped
		}

		return damage,mod,flags,towound,toburn,tostun,tobreak;
	}



	void DestroyRadBoots(){
	//if everything works perfectly, this should never happen
		destroy();
		if(owner){
			owner.A_TakeInventory("PowerIronFeet");
			owner.A_StartSound("RadBoots/burst",CHAN_BODY,CHANF_OVERLAP);
		}
	}
}



class ProtectiveRadBoots:HDPickup{
	default{
		//$Category "Gear/Hideous Destructor/Supplies"
		//$Title "anti-radiation boots"
		//$Sprite "RDBTA0"

		inventory.pickupmessage "You got the anti-radiation boots!";
		inventory.pickupsound "weapons/pocket";
		inventory.icon "RDBTA0";
		hdpickup.bulk ENC_RADBOOTS;
		tag "anti-radiation boots";
		hdpickup.refid HDLD_RADBOOTS;
	}

	override void DetachFromOwner(){
		owner.A_TakeInventory("ProtectiveRadBoots");
		owner.A_TakeInventory("WornRadBoots");
		target=owner;
		super.DetachFromOwner();
	}

	override inventory CreateTossable(int amt){
		if(
			amount<2
			&&owner.findinventory("WornRadBoots")
		){
			owner.UseInventory(self);
			return null;
		}
		return super.CreateTossable(amt);
	}

	override bool BeforePockets(actor other){
	//this controls the 'fast-equip' mechanic when
	//holding Use instead of tapping to pick it up
	
		//put on the armour right away
		if(
			other.player
			&&other.player.cmd.buttons&BT_USE
			&&!other.findinventory("WornRadBoots")
		){
			wornlayer=STRIP_RADBOOTS;
			bool intervening=!HDPlayerPawn.CheckStrip(other,self,false);
			wornlayer=0;

			if(intervening)return false;

			HDArmour.ArmourChangeEffect(other,60);//default is 120
			let onr=HDPlayerPawn(other);


			int fff=HDF.TransferFire(other,other);
			if(fff){
				if(random(1,fff)>999999){
					other.A_StartSound("misc/fwoosh",CHAN_BODY,CHANF_OVERLAP);
					destroy();
					return true;
				}else{
					HDF.TransferFire(self,other);
					if(onr){
						onr.fatigue+=fff;
						onr.stunned+=fff;
					}
				}
			}


			other.A_GiveInventory("ProtectiveRadBoots");
			other.A_GiveInventory("WornRadBoots");
			destroy();
			return true;
		}
		return false;
	}
	override void DoEffect(){
		bfitsinbackpack=(amount!=1||!owner||!owner.findinventory("WornRadBoots"));
		super.doeffect();
	}
	states{
	spawn:
		RDBT A 1;
		RDBT A -1{
			if(!target)return;
			HDF.TransferFire(target,self);
		}
	use:
		TNT1 A 0{
			let owrs=wornradboots(findinventory("WornRadBoots"));
			if(owrs){
				if(!HDPlayerPawn.CheckStrip(self,owrs))return;
			}else{
				invoker.wornlayer=STRIP_RADBOOTS+1;
				if(!HDPlayerPawn.CheckStrip(self,invoker)){
					invoker.wornlayer=0;
					return;
				}
				invoker.wornlayer=0;
			}

			HDArmour.ArmourChangeEffect(self,60);//default is 120
			let onr=HDPlayerPawn(self);
			if(!countinv("WornRadBoots")){
				int fff=HDF.TransferFire(self,self);

				if(fff){

					if(random(1,fff)>999999){
						A_StartSound("misc/fwoosh",CHAN_BODY,CHANF_OVERLAP);
						A_TakeInventory("ProtectiveRadBoots",1);
						return;
					}else{

						HDF.TransferFire(self,null);
						if(onr){
							onr.fatigue+=fff;
							onr.stunned+=fff;
						}
					}
				}
				A_GiveInventory("WornRadBoots");
			}else{
				actor a;int b;
				inventory wrs=findinventory("WornRadBoots");
				[b,a]=A_SpawnItemEx("ProtectiveRadBoots",0,0,height*0.5,0.2,0,2);
				if(a && wrs){
				
/*	
					//transfer sticky fire
					if(wrs.stamina){
						let aa=HDActor(a);
						if(aa)aa.A_Immolate(a,self,wrs.stamina);
					}
*/
					//transfer heat
					let hhh=heat(findinventory("heat"));
					if(hhh){
						double realamount=hhh.realamount;
						double intosuit=clamp(realamount*0.9,0,min(200,realamount));
						let hhh2=heat(a.GiveInventoryType("heat"));
						
						/*
					
						if(hhh2){
							hhh2.realamount+=intosuit;
							hhh.realamount=max(0,hhh.realamount-intosuit);
						}
						
						*/				
					}
					vel.z+=0.2;
					vel.xy+=(cos(angle),sin(angle))*0.7;
				}
				A_TakeInventory("WornRadBoots");
			}
			player.crouchfactor=min(player.crouchfactor,0.7);
		}fail;
	}
}
