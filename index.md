<p align="justify">
In this work, we (1) train the distributed representation of words using combinations of both general text data and music-specific data and (2) evaluate the system in terms of how they associate listening contexts with musical compositions. 
</p>

### Overview
<p align="justify">
MusicMusic listeners typically rely on a combination of listening contexts to find music including elements of mood, theme, time of day, location and activity. This scenario can be handled by defining a dictionary of contextual terms and directly associating them with music as a class label. However, such a music tagging approach (i.e., multi-label classification) is severely limited in considering contextual expression complexities that listeners can use from a natural language perspective. For example, a listener may use `club' to search for electronic dance music, and unless a model is trained with this specific word, it is not possible to consider the word as a query string. This issue has been addressed by representing tag words with embedding vectors and associating them with music in several different settings such as zero-shot learning \cite{choi2019zero}, query-by-blending and multi-task music representation learning. The aforementioned approaches were based on system training utilizing word embedding with either general text (e.g., Wikipedia or Gigaword) or music-specific corpus (e.g., tags, lyrics, artist IDs, track IDs). What is noteworthy here is that the general text training approach is limited in reflecting "musical" dimensions, whereas music-specific corpus limits incorporation of listening contexts which are not directly related to music while simultaneously suffering from small vocabulary size. 
</p>

![Model Architecture Ver 5 small artboard 2](./assets/img/figure1.png)
<p align="center">Figure.1 Train W2V and T-sne Visualization</p>

### Visualization
<p align="justify">

The t-SNE plot in Figure 1 provides a more intuitive  example on the result. We used two music genre terms 'electronic' and 'house' and three listening context terms 'club', 'club_dance', and 'partying'. In Wikipedia, they spread apart having only 'house' and 'club' close together. In the music corpus, the two genre terms and 'club' and 'club_dance' are tightly clustered while having 'partying' away. In the music corpus with Wikipedia, the context term 'partying' also becomes closer to the two genres and other context terms. This indicates that using both general and music-specific data provides more balanced correlation between music and listening context.
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
        <th> club </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> club,house,<br/> electronic</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_house_electornic/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_house_electornic/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_house_electornic/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> club,electronic,<br/> summer</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_electronic_summer/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_electronic_summer/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_electronic_summer/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> energetic,rap, <br/> exercise_workout</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_rap_exercise_workout/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_rap_exercise_workout/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_rap_exercise_workout/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> energetic,pop_rock,<br/> excercise_workout </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_pop_rock_exercise_workout/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_pop_rock_exercise_workout/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_pop_rock_exercise_workout/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> happy,jazz,cafe </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/happy_jazz_cafe/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/happy_jazz_cafe/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/happy_jazz_cafe/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> sad,jazz,cafe </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/sad_jazz_cafe/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/sad_jazz_cafe/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/sad_jazz_cafe/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> forest,ambient</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_ambient/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_ambient/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_ambient/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> forest,soundtrack</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_soundtrack/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_soundtrack/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_soundtrack/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>