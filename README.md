<If Condition="Me.FreeBagSlots &lt; Settings.Instance.VendorMinBagSlots &amp;&amp; (SpellManager.CanCast(61425) || SpellManager.CanCast(61447) || SpellManager.CanCast(122708))" >

	<If Condition="SpellManager.CanCast(61425) || SpellManager.CanCast(61447) || SpellManager.CanCast(122708)" > <!-- Traveler's + Yak -->
		<CustomBehavior File="WaitTimer" WaitTime="750" />
		<CustomBehavior File="RunCode" Code="if (Me.KnowsSpell(61425)) { Mount.SummonMount(61425); } else if (Me.KnowsSpell(61447)) { Mount.SummonMount(61447); } else { Mount.SummonMount(122708); }" />
		<CustomBehavior File="WaitTimer" WaitTime="2000" />

		<CustomBehavior File="InteractWith" MobId1="32639" MobId2="32641" MobId3="62822" WaitTime="1000" />
		
		<CustomBehavior File="RunCode" >
		<![CDATA[
			foreach (WoWItem i in Me.BagItems)
			{
				if (i != null && i.Entry != 6948 && !(Contains(Settings.Instance.ProtectedItemNames, i.Quality.ToString()) || Contains(Settings.Instance.ProtectedItemNames, i.Name) || Contains(Settings.Instance.ProtectedItemNames, i.Entry.ToString())) && !Contains(Settings.Instance.DepositItemNames, i.Name) && !Me.Combat && !Me.IsDead && !Me.IsGhost && MerchantFrame.Instance.IsVisible)
					i.UseContainerItem();
					StyxWoW.SleepForLagDuration();
			}
			Lua.DoString("RepairAllItems();");
		]]>
		</CustomBehavior>
	</If>

	<!-- Add Repair Bot support // Jeeves // Portable Mailboxes // etc -->
	
</If>
