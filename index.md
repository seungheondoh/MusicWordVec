<p align="justify">
This page is demo of MusicWordVec: Embedding for Musical Context.
</p>

### Overview
<p align="justify">
In this paper, we propose music domain specific word embedding using music corpus and wiki. music corpus is composed of amazon album review, allmusic semantic tag, and million song meta data. Each data is linked to song level using MSD track id and MusicBrainz ID. In the case of amazon album review, it contains information about the reason why users purchased this album and the mood, time, location, and activity associated with the song(Oramas et al.,2017). This music context information is linked to common natural language. In the case of allmusic semantic tag, annotations are provided for music term genre, style and context term mood and theme(Schindler & Knees, 2019). For million song meta data, track id and artist is exist(BertinMahieux et al., 2011). This music corpus merge with wikipedia corpus and is mapped to the same embedding space by distributional hypothesis. In figure1, central word ”club” co-occurrence with “sexy” and ”electronic”. According to color notation, ”club” can appear in both MuMu review text and Allmusic theme tags. Even clubs can appear in wiki corpus. Therefore, embedding word can learn from five different musical aspect.
</p>

![Model Architecture Ver 5 small artboard 2](./assets/img/figure.png)
<p align="center">Figure.1 Train W2V and T-sne Visualization</p>

### Results
<p align="justify">
For evaluation, all tags of test tag sets become queries. Each query got the tag co-occurrence information from data set. Tag co-occurrence assume a relevant label. When calculating mAP, 10 most frequent co-occurrence tags are used. Embedding calculates the tag to tag cosine similarity. This cosine similarity assume predict value of evaluation. We compute mean average precision and pearson correlation between relevant labels and predicts. At the same time, we also compare cosine similarity to relevant word pairs.
</p>

### Retrieval Result

<script>
function pauseOthers(ele) {
    $("audio").not(ele).each(function (index, audio) {audio.pause();});
}
</script>

<style>
.main-content table {
    display: inline-table;
}
table {
    table-layout:fixed;
    width: 100%;
    overflow: hidden;
}
#player{
    width: 100%;
}
</style>

<table>
    <tr>
        <th> Query </th>
        <th> Similar Song 1 </th>
        <th> Similar Song 2 </th>
        <th> Similar Song 3 </th>
    </tr>
    <tr>
        <th> "club" <br> location </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> "club","house","electronic" <br> location, genre, genre </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_house_electornic/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_house_electornic/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_house_electornic/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> "club","electronic","summer" <br> location, time, genre </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_electronic_summer/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_electronic_summer/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_electronic_summer/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> 'happy','jazz','cafe' <br> mood, genre, location </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/happy_jazz_cafe/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/happy_jazz_cafe/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/happy_jazz_cafe/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> 'sad','jazz','cafe' <br> mood, genre, location </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/sad_jazz_cafe/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/sad_jazz_cafe/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/sad_jazz_cafe/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> 'energetic','rap','exercise_workout' <br> mood, genre, activity </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_rap_exercise_workout/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_rap_exercise_workout/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_rap_exercise_workout/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> 'energetic','pop_rock','excercise_workout' <br> mood, genre, activity </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_pop_rock_exercise_workout/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_pop_rock_exercise_workout/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_pop_rock_exercise_workout/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> 'forest','ambient' <br> object, genre </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_ambient/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_ambient/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_ambient/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> 'forest','soundtrack' <br> object, genre </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_soundtrack/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_soundtrack/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_soundtrack/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>