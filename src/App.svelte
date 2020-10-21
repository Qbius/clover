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

	let clover = 0;
	let purity = 0;

	let glasses = 1;
	let predatory = 0;
	let scythe = 0;
	let dagger = 1;
	let stun = 1;
	let sticky = 1;
	let bandolier = 1;
	let meathook = 1;

	let cell = 0;
	let gesture = 0;

	let tougher = 1;
	let guillotine = 1;
</script>

<main>
	<div id="content">
		<Grouping caption="procs/drops">
			<div slot="header" style="display: flex; width: 65px; justify-content: space-between;">
				<Icon src="/57_Leaf_Clover.png" tier="legendary" size="29" hasborder count bind:value={clover}></Icon>
				<Icon src="/Purity.png" tier="lunar" size="29" hasborder count bind:value={purity}></Icon>
			</div>

			<Label caption="Crit chance" value={chance(0.01 + 0.1 * glasses + ((predatory > 0) ? 0.05 : 0) + ((scythe > 0) ? 0.05 : 0), clover, purity)}>
				<Icon src="/Lens-Maker's_Glasses.png" tier="common" size="64" count bind:value={glasses}></Icon>
				<Icon src="/Predatory_Instincts.png" tier="uncommon" size="64" count bind:value={predatory}></Icon>
				<Icon src="/Harvester's_Scythe.png" tier="uncommon" size="64" count bind:value={scythe}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(0.15 * dagger, clover, purity)}>
				<Icon src="/Tri-Tip_Dagger.png" tier="common" size="64" count bind:value={dagger}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(1 - 1 / (1 + 0.05 * stun), clover, purity)}>
				<Icon src="/Stun_Grenade.png" tier="common" size="64" count bind:value={stun}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(0.05 * sticky, clover, purity)}>
				<Icon src="/Sticky_Bomb.png" tier="common" size="64" count bind:value={sticky}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(0.1, clover, purity)}>
				<Icon src="/AtG_Missile_Mk_1.png" tier="uncommon" size="64"></Icon>
				<Icon src="/Molten_Perforator.png" tier="boss" size="64"></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(0.25, clover, purity)}>
				<Icon src="/Ukulele.png" tier="uncommon" size="64"></Icon>
			</Label>
			<Label caption="Chance to drop" value={chance(1 - 1 / Math.pow(1 + bandolier, 0.33), clover, purity)}>
				<Icon src="/Bandolier.png" tier="uncommon" size="64" count bind:value={bandolier}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(0.07, clover, purity)}>
				<Icon src="/Happiest_Mask.png" tier="legendary" size="64"></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(1 - 1 / (1 + 0.2 * meathook), clover, purity)}>
				<Icon src="/Sentient_Meat_Hook.png" tier="legendary" size="64" count bind:value={meathook}></Icon>
			</Label>
			<Label caption="Chance to proc" value={chance(0.00025, clover, purity)}>
				<Icon src="/Ifrit's_Distinction.png" tier="legendary" size="64"></Icon>
			</Label>
			<Label caption="Chance to drop" value={chance(0.01, clover, purity)}>
				<Icon src="/Monster_Log_Enemy_Icon.png" tier="none" size="64"></Icon>
			</Label>
			<Label caption="Chance to drop" value={chance(0.03, clover, purity)}>
				<Icon src="/Monster_Log_Enemy_Icon.png" tier="none" size="64" caption="BOSS" smalltext></Icon>
			</Label>
		</Grouping>

		<Grouping caption="Equipment">
			<div slot="header" style="display: flex; width: 65px; justify-content: space-between;">
				<Icon src="/Fuel_Cell.png" tier="uncommon" size="29" hasborder count bind:value={cell}></Icon>
				<Icon src="/Gesture_of_the_Drowned.png" tier="lunar" size="29" hasborder count bind:value={gesture}></Icon>
			</div>
		</Grouping>

		<Grouping caption="Misc.">
			<Label caption="Chance to block" value={stylize_probability(1 - 1 / (1 + 0.15 * tougher))}>
				<Icon src="/Tougher_Times.png" tier="common" size="64" count bind:value={tougher}></Icon>
			</Label>
			<Label caption="Execute threshold" value={stylize_probability(1 - 1 / (1 + 0.13 * guillotine))}>
				<Icon src="/Old_Guillotine.png" tier="uncommon" size="64" count bind:value={guillotine}></Icon>
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

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	#content {
		margin: auto;
		width: 100%;

		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.upfront {
		position: absolute;
		z-index: 1000;
	}



	.infotext {
		margin: auto;
		font-size: 12px;
	}
</style>