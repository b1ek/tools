+++
+++

# username generator

<div class=card>
    <input type=text id=output readonly placeholder=output style='font-family:monospace'>
    <input type=number id=seed>
    <input type=number id=length value=6>
</div>

<script>
    (() => {
        const output = document.getElementById('output');
        const seed = document.getElementById('seed');
        const length = document.getElementById('length');

        const rainbow = [476407774,133080325,1566090489,1536534254,1930409622,532477246,1641965280,1634422546,241832343,657664171,1555825314,579218182,877433288,353284366,75436354,2004658845,1371646375,714304706,1953593781,1772091558,1340408577,316326684,1559123068,1534686876,1056191243,340546297,1491278682,954900622,826586610,836091870,1791473959,685407888,1260359320,1512520784,2061773085,2047961844,219408498,258352442,1261246054,1732505125,670862131,753862595,1908902829,1619477604,393324733,1396774385,483479220,1077570134,1242667605,1131118711,1062351785,1078043497,710627024,530705297,1318792345,127584534,1553487327,1262331117,1595123247,1536517868,1951632163,1110404165,929339615,1652537868,1009596855,1620440524,159275543,379827117,422976696,1513648396,802864562,1841727635,402310305,18095913,393919589,64056783,569993468,1966372774,1403217273,841995459,168871026,2038346311,704061623,321951815,878253043,71011975,1483692273,1589633574,238532715,1083351627,2125146657,629227478,1565141318,628897691,1814306015,433797112,2132093503,1892276945,1394949053,1532444155,1728384568,188433414,49750295,2084184632,1720487028,147361456,1969738712,1175982035,1696138089,1958264056,51554077,466924313,154804881,2085095961,807702462,1181740914,900184250,1497911554,154370922,832344701,1415205394,1672992361,1023154571,518796357,469305683,555209373,371040282,610448916];

        seed.defaultValue = Math.floor(Math.random() * 1000000);

        function random(seed) {
            let x = seed + rainbow[seed % (rainbow.length - 1)];
            return Math.floor(x * 1664525 + 1013904223) % 4294967296;
        }
        function pick(array, seed) {
            return array[random(seed) % (array.length - 1)];
        }
        function genWord(seed, len) {
            let word = '';

            for (let i = 0; i != len; i++) {
                let set = consonants;
                if (i % 2 !== 0) {
                    set = vowels;
                }
                const p = pick(set, seed);
                word += p;
                seed = random(seed) + pick(rainbow, seed);
            }
            return word;
        }
        const consonants = 'bcdfghjklmnpqrstvwxz';
        const vowels = 'aeiou';

        function change() {
            output.value = genWord(parseInt(seed.value), parseInt(length.value))
        }
        seed.onchange = change;
        length.onchange = change;
        change();

        globalThis.genWord = genWord;
    })();
</script>