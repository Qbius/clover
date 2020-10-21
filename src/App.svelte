<script>
	import Icon from './Icon.svelte';
	import Label from './Label.svelte';
	import Grouping from './Grouping.svelte';

	function stylize_probability(p) {
		return `${Number((Math.min(p, 1) * 100).toFixed(2))}%`;
	}

	function chance(p, clovers, purities) {
		const luck = clovers - purities;
		const probbase = Math.pow((luck >= 0) ? 1 - p : p, Math.abs(luck) + 1);
		return stylize_probability((luck >= 0) ? 1 - probbase : probbase)
	}

	function cooldown(c, cell, gestures) {
		const proper_c = c * Math.pow(0.85, cell + Math.max(gestures - 1, 0)) * ((gestures > 0) ? 0.5 : 1);
		return `${Math.round(proper_c)}s`;
	}

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
</script>

<main>
	<div id="content">
		<Grouping caption="procs/drops" vertical>
			<div slot="header" style="display: flex; width: 65px; justify-content: space-between;">
				<Icon src="/57_Leaf_Clover.png" tier="legendary" size="29" hasborder count bind:value={clover}></Icon>
				<Icon src="/Purity.png" tier="lunar" size="29" hasborder count bind:value={purity}></Icon>
			</div>
			<div style="display: flex; justify-content: space-evenly; margin-bottom: 5px; ">
				<Icon src="/AtG_Missile_Mk_1.png" tier="uncommon" size="58" caption={chance(0.1, clover, purity)} smallertext></Icon>
				<Icon src="/Molten_Perforator.png" tier="boss" size="58" caption={chance(0.1, clover, purity)} smallertext></Icon>
				<Icon src="/Ukulele.png" tier="uncommon" size="58" caption={chance(0.25, clover, purity)} smallertext></Icon>
				<Icon src="/Happiest_Mask.png" tier="legendary" size="58" caption={chance(0.07, clover, purity)} smallertext></Icon>
			</div>
			<Label caption="Crit chance" value={chance(0.01 + 0.1 * glasses + (predatory ? 0.05 : 0) + (scythe ? 0.05 : 0) + (shatterspleen ? 0.05 : 0), clover, purity)}>
				<Icon src="/Lens-Maker's_Glasses.png" tier="common" size="58" count bind:value={glasses}></Icon>
				<div style="display: flex; flex-direction: column;">
					<Icon src="/Predatory_Instincts.png" tier="uncommon" size="18" onoff bind:boolean={predatory}></Icon>
					<Icon src="/Harvester's_Scythe.png" tier="uncommon" size="18" onoff bind:boolean={scythe}></Icon>
					<Icon src="/Shatterspleen.png" tier="boss" size="18" onoff bind:boolean={shatterspleen}></Icon>
				</div>
			</Label>
			<Label caption="Chance to proc" value={chance(0.15 * dagger, clover, purity)}>
				<Icon src="/Tri-Tip_Dagger.png" tier="common" size="58" count bind:value={dagger}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(1 - 1 / (1 + 0.05 * stun), clover, purity)}>
				<Icon src="/Stun_Grenade.png" tier="common" size="58" count bind:value={stun}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(0.05 * sticky, clover, purity)}>
				<Icon src="/Sticky_Bomb.png" tier="common" size="58" count bind:value={sticky}></Icon>
			</Label>
			<Label caption="Chance to drop" value={chance(1 - 1 / Math.pow(1 + bandolier, 0.33), clover, purity)}>
				<Icon src="/Bandolier.png" tier="uncommon" size="58" count bind:value={bandolier}></Icon>
			</Label>
			<Label caption="Chance to drop" value={chance(0.04 * tome, clover, purity)}>
				<Icon src="/Ghor's_Tome.png" tier="uncommon" size="58" count bind:value={tome}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(1 - 1 / (1 + 0.2 * meathook), clover, purity)}>
				<Icon src="/Sentient_Meat_Hook.png" tier="legendary" size="58" count bind:value={meathook}></Icon>
			</Label>
			<Label caption="Chance to drop" value={chance(0.00025, clover, purity)}>
				<div style="width: 180px; height: 60px; padding-left: 1px; display: flex; align-items: center; justify-content: space-between;">
					<Icon src="/Ifrit's_Distinction.png" tier="equipment" size="32"></Icon>
					<Icon src="/Silence_Between_Two_Strikes.png" tier="equipment" size="32"></Icon>
					<Icon src="/Her_Biting_Embrace.png" tier="equipment" size="32"></Icon>
					<Icon src="/N'kuhana's_Retort.png" tier="equipment" size="32"></Icon>
					<Icon src="/Spectral_Circlet.png" tier="equipment" size="32"></Icon>
				</div>
			</Label>
			<Label caption="Monster drop" value={chance(0.01, clover, purity)} extras={[["Boss drop", chance(0.03, clover, purity)]]}>
				<Icon src="/Monster_Log_Enemy_Icon.png" tier="none" size="58"></Icon>
			</Label>
		</Grouping>

		<Grouping caption="Equipment">
			<div slot="header" style="display: flex; width: 65px; justify-content: space-between;">
				<Icon src="/Fuel_Cell.png" tier="uncommon" size="29" hasborder count bind:value={cell}></Icon>
				<Icon src="/Gesture_of_the_Drowned.png" tier="lunar" size="29" hasborder count bind:value={gesture}></Icon>
			</div>
			<Icon src="/Disposable_Missile_Launcher.png" tier="equipment" size="58" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Foreign_Fruit.png" tier="equipment" size="58" caption={cooldown(45, cell, gesture)} smalltext adnotation="10s duration"></Icon>
			<Icon src="/Primordial_Cube.png" tier="equipment" size="58" caption={cooldown(60, cell, gesture)} smalltext></Icon>
			<Icon src="/Ocular_HUD.png" tier="equipment" size="58" caption={cooldown(60, cell, gesture)} smalltext adnotation="8s duration"></Icon>
			<Icon src="/The_Back-up.png" tier="equipment" size="58" caption={cooldown(100, cell, gesture)} smalltext adnotation="25s duration"></Icon>
			<Icon src="/Preon_Accumulator.png" tier="equipment" size="58" caption={cooldown(140, cell, gesture)} smalltext></Icon>
			<Icon src="/Milky_Chrysalis.png" tier="equipment" size="58" caption={cooldown(60, cell, gesture)} smalltext adnotation="15s duration"></Icon>
			<Icon src="/Royal_Capacitor.png" tier="equipment" size="58" caption={cooldown(20, cell, gesture)} smalltext></Icon>
			<Icon src="/Gnarled_Woodsprite.png" tier="equipment" size="58" caption={cooldown(15, cell, gesture)} smalltext></Icon>
			<Icon src="/Radar_Scanner.png" tier="equipment" size="58" caption={cooldown(45, cell, gesture)} smalltext adnotation="10s duration"></Icon>
			<Icon src="/Eccentric_Vase.png" tier="equipment" size="58" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Blast_Shower.png" tier="equipment" size="58" caption={cooldown(20, cell, gesture)} smalltext></Icon>
			<Icon src="/Volcanic_Egg.png" tier="equipment" size="58" caption={cooldown(30, cell, gesture)} smalltext adnotation="5s duration"></Icon>
			<Icon src="/Jade_Elephant.png" tier="equipment" size="58" caption={cooldown(45, cell, gesture)} smalltext adnotation="5s duration"></Icon>
			<Icon src="/Sawmerang.png" tier="equipment" size="58" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Recycler.png" tier="equipment" size="58" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Super_Massive_Leech.png" tier="equipment" size="58" caption={cooldown(60, cell, gesture)} smalltext adnotation="8s duration"></Icon>
			<Icon src="/Gorag's_Opus.png" tier="equipment" size="58" caption={cooldown(45, cell, gesture)} smalltext adnotation="7s duration"></Icon>
			<Icon src="/Forgive_Me_Please.png" tier="equipment" size="58" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Glowing_Meteorite.png" tier="lunar" size="58" caption={cooldown(140, cell, gesture)} smalltext adnotation="20s duration"></Icon>
			<Icon src="/Helfire_Tincture.png" tier="lunar" size="58" caption={cooldown(45, cell, gesture)} smalltext adnotation="12s duration"></Icon>
			<Icon src="/Effigy_of_Grief.png" tier="lunar" size="58" caption={cooldown(45, cell, gesture)} smalltext></Icon>
			<Icon src="/Spinel_Tonic.png" tier="lunar" size="58" caption={cooldown(60, cell, gesture)} smalltext adnotation="20s duration"></Icon>

		</Grouping>

		<Grouping caption="Misc." vertical>
			<Label caption="Chance to block" value={stylize_probability(1 - 1 / (1 + 0.15 * tougher))}>
				<Icon src="/Tougher_Times.png" tier="common" size="58" count bind:value={tougher}></Icon>
			</Label>
			<Label caption="Execute threshold" value={stylize_probability(1 - 1 / (1 + 0.13 * guillotine))}>
				<Icon src="/Old_Guillotine.png" tier="uncommon" size="58" count bind:value={guillotine}></Icon>
			</Label>
			<Label caption="White item" value={rusted_white} extras={[["Green item", rusted_green], ["Red item", rusted_red]]}>
				<Icon src="/Rusted_Key.png" tier="common" size="58" count bind:value={rusted}></Icon>
			</Label>
		</Grouping>
	</div>
</main>

<style>
	main {
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;

		display: flex;
		justify-content: center;
	}

	#content {
		margin: auto;
		width: 100%;

		display: flex;
		justify-content: space-between;
		align-items: flex-start;
		flex-wrap: wrap;
	}

@media (min-width: 640px) {
	main {
		max-width: none;
	}

	#content {
		flex-wrap: nowrap;
	}
}
</style>