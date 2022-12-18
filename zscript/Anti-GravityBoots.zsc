//Based off Radsuit code from Hideous Destructor
//-------------------------------------------------
// Anti-Gravity Boots
//-------------------------------------------------

const STRIP_ANTIGRAVBOOTS=1500;
const ENC_ANTIGRAVBOOTS=35;
const HDLD_ANTIGRAVBOOTS="AGV";//Anti-GraVity

const ANTIGRAV_MAXCHARGE=500;


class WornAntiGravBoots:HDDamageHandler{
	int antigrav_charge;

	default{
		+nointeraction;
		+noblockmap;
		-hdpickup.fullcoverage
		//this flag controls whether you can bandage 
		//with it equipped or not
	
		-inventory.isarmor
		inventory.maxamount 1;inventory.amount 1;
		HDDamageHandler.priority 1000;
		HDPickup.wornlayer STRIP_ANTIGRAVBOOTS;
		HDPickup.overlaypriority 150;
		tag "anti-gravity boots";
	}
	states{spawn:TNT1 A 0;stop;}

	override void postbeginplay(){
		super.postbeginplay();
		antigrav_charge=ANTIGRAV_MAXCHARGE;
	}

	override inventory createtossable(int amt){
		let rrr=owner.findinventory("AntiGravBoots");
		if(rrr)owner.useinventory(rrr);else destroy();
		return null;
	}
	override void attachtoowner(actor owner){
		if(!owner.countinv("AntiGravBoots"))
			owner.A_GiveInventory("AntiGravBoots");
			//owner.gravity=HDCONST_GRAVITY/3;
		super.attachtoowner(owner);
	}
	override void DetachFromOwner(){
		owner.A_TakeInventory("AntiGravBoots",1);
		HDArmour.ArmourChangeEffect(owner,10);
		//this triggers the stun effect when removing gear
		//the number seems to control how long the stun lasts

		owner.gravity=HDCONST_GRAVITY;
		super.DetachFromOwner();
	}

	override void DoEffect(){
	//stuff here happens every tic
		if(stamina>0)stamina--;

		let hp=HDPlayerPawn(owner);
        
        //the boots should recharge if you're not moving
		if(hp&&antigrav_charge>0&&countinv("IsMoving")>3){
			antigrav_charge--;

            //if the boots have a charge, they'll 
            //lower your gravity
			if(!antigrav_charge<1){
				owner.gravity=HDCONST_GRAVITY/3;
			}
			else owner.gravity=HDCONST_GRAVITY;

		}//if the player is still, the boots will recharge
		else if(antigrav_charge<ANTIGRAV_MAXCHARGE)
		    antigrav_charge++;
		    
		if(!hp){destroy();return;}
	}

	override double RestrictSpeed(double speedcap){
	//this changes how fast a player can move while wearing this
		return min(speedcap, 2);//default is 1.8
	}
	 
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
			"AGRVA0",
			am?(11,137):(84,-5),
			am?sb.DI_TOPLEFT:
			(sb.DI_SCREEN_CENTER_BOTTOM|sb.DI_ITEM_CENTER_BOTTOM)
		);
        
        //draws charge amount on boots sprite
		sb.drawstring(
			sb.pnewsmallfont,sb.formatnumber(antigrav_charge/5),
			am?(14,136):(84,-10),
			am?(sb.DI_TOPLEFT|sb.DI_TEXT_ALIGN_RIGHT)
			:(sb.DI_SCREEN_CENTER_BOTTOM|sb.DI_TEXT_ALIGN_RIGHT),
			Font.CR_RED,scale:(0.5,0.5)
		);
	}


	void DestroyAntiGravBoots(){
	//if everything works perfectly, this should never happen
		destroy();
		if(owner){
			owner.A_TakeInventory("PowerIronFeet");
			owner.A_StartSound("AntiGravBoots/burst",CHAN_BODY,CHANF_OVERLAP);
		}
	}
}



class AntiGravBoots:HDPickup{
	default{
		//$Category "Gear/Hideous Destructor/Supplies"
		//$Title "anti-gravity boots"
		//$Sprite "AGRVA0"

		inventory.pickupmessage "You got the anti-gravity boots!";
		inventory.pickupsound "weapons/pocket";
		inventory.icon "AGRVA0";
		hdpickup.bulk ENC_ANTIGRAVBOOTS;
		tag "anti-gravity boots";
		hdpickup.refid HDLD_ANTIGRAVBOOTS;
	}

	override void DetachFromOwner(){
		owner.A_TakeInventory("AntiGravBoots");
		owner.A_TakeInventory("WornAntiGravBoots");
		target=owner;
		super.DetachFromOwner();
	}

	override inventory CreateTossable(int amt){
		if(
			amount<2
			&&owner.findinventory("WornAntiGravBoots")
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
			&&!other.findinventory("WornAntiGravBoots")
		){
			wornlayer=STRIP_ANTIGRAVBOOTS;
			bool intervening=!HDPlayerPawn.CheckStrip(other,self,false);
			wornlayer=0;

			if(intervening)return false;

			HDArmour.ArmourChangeEffect(other,60);//default is 120
			other.A_GiveInventory("AntiGravBoots");
			other.A_GiveInventory("WornAntiGravBoots");
			destroy();
			return true;
		}
		return false;
	}
	override void DoEffect(){
		bfitsinbackpack=(amount!=1||!owner||!owner.findinventory("WornAntiGravBoots"));
		super.doeffect();
	}
	states{
	spawn:
		AGRV A 1;
		AGRV A -1{
			if(!target)return;
			HDF.TransferFire(target,self);
		}
	use:
		TNT1 A 0{
			let owrs=wornantigravboots(findinventory("WornAntiGravBoots"));
			if(owrs){
				if(!HDPlayerPawn.CheckStrip(self,owrs))return;
			}else{
				invoker.wornlayer=STRIP_ANTIGRAVBOOTS+1;
				if(!HDPlayerPawn.CheckStrip(self,invoker)){
					invoker.wornlayer=0;
					return;
				}
				invoker.wornlayer=0;
			}

			HDArmour.ArmourChangeEffect(self,10);//default is 120
			let onr=HDPlayerPawn(self);
			if(!countinv("WornAntiGravBoots")){
				A_GiveInventory("WornAntiGravBoots");
			}else{
				actor a;int b;
				inventory wrs=findinventory("WornAntiGravBoots");
				[b,a]=A_SpawnItemEx("AntiGravBoots",0,0,height*0.5,0.2,0,2);
				if(a && wrs){
					vel.z+=0.2;
					vel.xy+=(cos(angle),sin(angle))*0.7;
				}
				A_TakeInventory("WornAntiGravBoots");
			}
			player.crouchfactor=min(player.crouchfactor,0.7);
		}fail;
	}
}