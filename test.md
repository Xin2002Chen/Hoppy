## Linjärtidssortering när det finns många dubbletter

**I ord:** Gå igenom varje element, i, i listan och lägg till elementet till HashMap med key i och uppdatera antal förekomster, därefter gå igenom varje key och lägg till elementet till den sorterade listan med dess respektive frekvens.

**Pseudokod:**
<pre><code> void sort(int[] nums):
	HashMap count = new HashMap();
    int n = nums.length;

	//Count all elements and their respective frequency
    for int i in range(n):
		if(!count.containsKey(nums[i])):
			count.put(nums[i], 0);
		count.put(nums[i], count.get(nums[i]+1));
	
    //Go through each key in the map, assume the keys are already sorted
	int counter = 0;
    for int key in count.keySet:
        int currentFrequency = key.value;

        for int i in range(currentFrequency):
			nums[counter + i] = key;
		counter += currentFrequency;
</code></pre>

Algoritmen är **O(n + klog(k))** , då det tar O(1) tid för att skapa en tom HashMap, O(n) tid att gå igenom hela listan, samt de flesta programmeringsspråk har en inbyggd sort funktion som är O(nlog(n)). Då vi har k-stycken distinkta tal, har vi k-stycken "keys". Alltså kommer den inbyggda algoritmen som sorterar keys ge oss O(klog(k)) tidskomplexitet. Slutligen, har vi en för-slinga för att kolla upp frekvensen för de olika keys vår HashMap innehåller, som ger en förväntad tid på O(1) inom en singel iteration och däreter fyller vi i listan med de sorterade talen. Alltså får vi O(n) förväntad tid för att utföra för-slingan. <br/> Tillsammans ger detta oss förväntad tid på **O(n + klog(k))** för hela algoritmen.

**Låt oss slutligen undersöka för vilka k som algoritmen blir linjär:** vi vill att n ska dominera, dvs, n >= klog(k), samtidigt som k kan inte vara större än n, dvs k<=n. Om man plottar grafen till ovanstående villkor (under antagandet att det inte finns några koefficienter i någon av leden) ser vi att detta gäller för k som är lika med eller mindre basen av log. Då man brukar använda log i bas 2 i datalogi, verkar det som att redan vid två element blir algoritmen k*log(k), och listan är redan sorterad när k=1. Alltså gäller det för alla k som algoritmen är **O(n + klog(k))**, aldrig linjär!
