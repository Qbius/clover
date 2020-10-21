<script>
	import Icon from './Icon.svelte';
	import Label from './Label.svelte';
	import Grouping from './Grouping.svelte';

	function stylize_probability(p) {
		return `${Number((Math.min(p, 1) * 100).toFixed(2))}%`;
	}

	function apply_luck(p, clovers, purities) {
		const luck = clovers - purities;
		const probbase = Math.pow((luck >= 0) ? 1 - p : p, Math.abs(luck) + 1);
		return (luck >= 0) ? 1 - probbase : probbase;
	}

	function chance(p, clovers, purities) {
		return stylize_probability(apply_luck(p, clovers, purities));
	}

	function cooldown(c, cell, gestures) {
		const proper_c = c * Math.pow(0.85, cell + Math.max(gestures - 1, 0)) * ((gestures > 0) ? 0.5 : 1);
		return `${Math.round(proper_c)}s`;
	}

	let proc_coefficient = 1;

	let clover = 0;
	let purity = 0;

	let glasses = 1;
	let predatory = false;
	let scythe = false;
	let shatterspleen = false;
	let dagger = 1;
	let stun = 1;
	let sticky = 1;
	let bandolier = 1;
	let tome = 1;
	let meathook = 1;

	let cell = 0;
	let gesture = 0;

	let tougher = 1;
	let guillotine = 1;
	let rusted = 1;
	$: rusted_net_rarity = 80 + 20 * rusted + rusted * rusted;
	$: rusted_white = (rusted > 0) ? stylize_probability(80 / rusted_net_rarity) : 'N/A';
	$: rusted_green = (rusted > 0) ? stylize_probability(20 * rusted / rusted_net_rarity) : 'N/A';
	$: rusted_red = (rusted > 0) ? stylize_probability(rusted * rusted / rusted_net_rarity) : 'N/A';

	$: iphonese = window.screen.width <= 240;
	$: eqperrow = iphonese ? 4 : 5;
	$: eqrowscount = Math.ceil(23 / eqperrow);
</script>

<main>
	<div id="content">
		<Grouping caption="procs/drops" rowspan>
			<div slot="header" style="display: flex; width: 65px; justify-content: space-between;">
				<Icon src="/57_Leaf_Clover.png" tier="legendary" size="29" hasborder count bind:value={clover}></Icon>
				<Icon src="/Purity.png" tier="lunar" size="29" hasborder count bind:value={purity}></Icon>
			</div>
			<div style="display: flex; justify-content: space-between; margin-bottom: 5px; margin-left: 5px; margin-right: 5px;">
				<Icon src="/AtG_Missile_Mk_1.png" tier="uncommon" size={iphonese ? '34' : '52'} caption={chance(0.1 * proc_coefficient, clover, purity)} smallertext></Icon>
				<Icon src="/Molten_Perforator.png" tier="boss" size={iphonese ? '34' : '52'} caption={chance(0.1 * proc_coefficient, clover, purity)} smallertext></Icon>
				<Icon src="/Ukulele.png" tier="uncommon" size={iphonese ? '34' : '52'} caption={chance(0.25 * proc_coefficient, clover, purity)} smallertext></Icon>
				<Icon src="/Happiest_Mask.png" tier="legendary" size={iphonese ? '34' : '52'} caption={chance(0.07, clover, purity)} smallertext></Icon>
				<Icon src="/Brittle_Crown.png" tier="lunar" size={iphonese ? '34' : '52'} caption={chance(0.3 * proc_coefficient, clover, purity)} smallertext></Icon>
			</div>
			<Label caption="Crit chance" value={chance(0.01 + 0.1 * glasses + (predatory ? 0.05 : 0) + (scythe ? 0.05 : 0) + (shatterspleen ? 0.05 : 0), clover, purity)}>
				<Icon src="/Lens-Maker's_Glasses.png" tier="common" size="58" count bind:value={glasses}></Icon>
				<div style="display: flex; flex-direction: column;">
					<Icon src="/Predatory_Instincts.png" tier="uncommon" size="18" onoff bind:boolean={predatory}></Icon>
					<Icon src="/Harvester's_Scythe.png" tier="uncommon" size="18" onoff bind:boolean={scythe}></Icon>
					<Icon src="/Shatterspleen.png" tier="boss" size="18" onoff bind:boolean={shatterspleen}></Icon>
				</div>
			</Label>
			<Label caption="Chance to proc" value={chance(0.15 * dagger * proc_coefficient, clover, purity)}>
				<Icon src="/Tri-Tip_Dagger.png" tier="common" size="58" count bind:value={dagger}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance((1 - 1 / (1 + 0.05 * stun)) * proc_coefficient, clover, purity)}>
				<Icon src="/Stun_Grenade.png" tier="common" size="58" count bind:value={stun}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(0.05 * sticky * proc_coefficient, clover, purity)}>
				<Icon src="/Sticky_Bomb.png" tier="common" size="58" count bind:value={sticky}></Icon>
			</Label>
			<Label caption="Chance to drop" value={chance(1 - 1 / Math.pow(1 + bandolier, 0.33), clover, purity)}>
				<Icon src="/Bandolier.png" tier="uncommon" size="58" count bind:value={bandolier}></Icon>
			</Label>
			<Label caption="Chance to drop" value={chance(0.04 * tome, clover, purity)}>
				<Icon src="/Ghor's_Tome.png" tier="uncommon" size="58" count bind:value={tome}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance((1 - 1 / (1 + 0.2 * meathook)) * proc_coefficient, clover, purity)}>
				<Icon src="/Sentient_Meat_Hook.png" tier="legendary" size="58" count bind:value={meathook}></Icon>
			</Label>
			<Label caption="Monster drop" value={chance(0.01, clover, purity)} extras={[["Boss drop", chance(0.03, clover, purity)]]}>
				<Icon src="/Monster_Log_Enemy_Icon.png" tier="none" size="58"></Icon>
			</Label>
			<Label caption="Chance to drop" value={chance(0.00025, clover, purity)}>
				<div style="display: flex; flex-direction: column; align-items: flex-start;">
					<div style="width: 90px; height: 30px; padding-left: 1px; display: flex; align-items: flex-end; justify-content: center;">
						<Icon src="/Ifrit's_Distinction.png" tier="equipment" size="28"></Icon>
						<Icon src="/Silence_Between_Two_Strikes.png" tier="equipment" size="28"></Icon>
						<Icon src="/Her_Biting_Embrace.png" tier="equipment" size="28"></Icon>
					</div>
					<div style="width: 90px; height: 30px; padding-left: 1px; display: flex; align-items: flex-start; justify-content: center;">
						<Icon src="/N'kuhana's_Retort.png" tier="equipment" size="28"></Icon>
						<Icon src="/Spectral_Circlet.png" tier="equipment" size="28"></Icon>
					</div>
				</div>
			</Label>
			<Label caption="Chance to get" value={stylize_probability(1 - apply_luck(0.8, clover, purity))}>
				<Icon src="/Tonic_Affliction.png" tier="none" size="58"></Icon>
			</Label>
			<Label caption="Chance to ignite" value={chance(0.5, clover, purity)} extras={[["Average stacks", Math.round(22 * apply_luck(0.5, clover, purity))]]}>
				<Icon src="Flamethrower.png" tier="none" size="58"></Icon>
			</Label>
		</Grouping>

		<Grouping caption="Equipment" wrap>
			<div slot="header" style="display: flex; width: 65px; justify-content: space-between;">
				<Icon src="/Fuel_Cell.png" tier="uncommon" size="29" hasborder count bind:value={cell}></Icon>
				<Icon src="/Gesture_of_the_Drowned.png" tier="lunar" size="29" hasborder count bind:value={gesture}></Icon>
			</div>
			<Icon src="/Disposable_Missile_Launcher.png" tier="equipment" size="52" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Foreign_Fruit.png" tier="equipment" size="52" caption={cooldown(45, cell, gesture)} smalltext adnotation="10s duration"></Icon>
			<Icon src="/Primordial_Cube.png" tier="equipment" size="52" caption={cooldown(60, cell, gesture)} smalltext></Icon>
			<Icon src="/Ocular_HUD.png" tier="equipment" size="52" caption={cooldown(60, cell, gesture)} smalltext adnotation="8s duration"></Icon>
			<Icon src="/The_Back-up.png" tier="equipment" size="52" caption={cooldown(100, cell, gesture)} smalltext adnotation="25s duration"></Icon>
			<Icon src="/Preon_Accumulator.png" tier="equipment" size="52" caption={cooldown(140, cell, gesture)} smalltext></Icon>
			<Icon src="/Milky_Chrysalis.png" tier="equipment" size="52" caption={cooldown(60, cell, gesture)} smalltext adnotation="15s duration"></Icon>
			<Icon src="/Royal_Capacitor.png" tier="equipment" size="52" caption={cooldown(20, cell, gesture)} smalltext></Icon>
			<Icon src="/Gnarled_Woodsprite.png" tier="equipment" size="52" caption={cooldown(15, cell, gesture)} smalltext></Icon>
			<Icon src="/Radar_Scanner.png" tier="equipment" size="52" caption={cooldown(45, cell, gesture)} smalltext adnotation="10s duration"></Icon>
			<Icon src="/Eccentric_Vase.png" tier="equipment" size="52" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Blast_Shower.png" tier="equipment" size="52" caption={cooldown(20, cell, gesture)} smalltext></Icon>
			<Icon src="/Volcanic_Egg.png" tier="equipment" size="52" caption={cooldown(30, cell, gesture)} smalltext adnotation="5s duration"></Icon>
			<Icon src="/Jade_Elephant.png" tier="equipment" size="52" caption={cooldown(45, cell, gesture)} smalltext adnotation="5s duration"></Icon>
			<Icon src="/Sawmerang.png" tier="equipment" size="52" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Recycler.png" tier="equipment" size="52" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Super_Massive_Leech.png" tier="equipment" size="52" caption={cooldown(60, cell, gesture)} smalltext adnotation="8s duration"></Icon>
			<Icon src="/Gorag's_Opus.png" tier="equipment" size="52" caption={cooldown(45, cell, gesture)} smalltext adnotation="7s duration"></Icon>
			<Icon src="/Forgive_Me_Please.png" tier="equipment" size="52" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Glowing_Meteorite.png" tier="lunar" size="52" caption={cooldown(140, cell, gesture)} smalltext adnotation="20s duration"></Icon>
			<Icon src="/Helfire_Tincture.png" tier="lunar" size="52" caption={cooldown(45, cell, gesture)} smalltext adnotation="12s duration"></Icon>
			<Icon src="/Effigy_of_Grief.png" tier="lunar" size="52" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Spinel_Tonic.png" tier="lunar" size="52" caption={cooldown(60, cell, gesture)} smalltext adnotation="20s duration"></Icon>
		</Grouping>

		<Grouping caption="Misc.">
			<Label caption="Chance to block" value={stylize_probability(1 - 1 / (1 + 0.15 * tougher))}>
				<Icon src="/Tougher_Times.png" tier="common" size="58" count bind:value={tougher}></Icon>
			</Label>
			<Label caption="Execute threshold" value={stylize_probability(1 - 1 / (1 + 0.13 * guillotine))}>
				<Icon src="/Old_Guillotine.png" tier="uncommon" size="58" count bind:value={guillotine}></Icon>
			</Label>
			<Label caption="White" value={rusted_white} extras={[["Green", rusted_green], ["Red", rusted_red]]} small>
				<Icon src="/Rusted_Key.png" tier="common" size="58" count bind:value={rusted}></Icon>
			</Label>
		</Grouping>
	</div>
</main>

<style>
	main {
		display: flex;
		justify-content: center;
	}

	#content {
		width: 100%;

		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;
	}

	.eq_row {
		margin-left: 4px;
		margin-right: 4px;
		display: flex;
		justify-content: center;
	}

@media (min-width: 640px) {
	main {
		max-width: none;
		height: 100vh;
	}

	#content {
		flex-direction: row;
		justify-content: center;
		align-items: flex-start;
	}
}
</style>