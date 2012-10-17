NReplayGain
============

A ReplayGain implementation in C# .NET

The API for calculating ReplayGain for a single track:
TrackGain trackGain = new TrackGain(44100, 16);
foreach (sampleSet in track) {
	trackGain.AnalyzeSamples(leftSamples, rightSamples)
}
double gain = trackGain.GetGain();
double peak = trackGain.GetPeak();

If you also need album gain:

AlbumGain albumGain = new AlbumGain();
foreach (track in tracks) {
	TrackGain trackGain = new TrackGain(44100, 16);
	foreach (sampleSet in track) {
		trackGain.AnalyzeSamples(leftSamples, rightSamples)
	}
	albumGain.AppendTrack(trackGain);
	double trackGain = trackGain.GetGain();
	double trackPeak = trackGain.GetPeak();
}
double albumGain = albumGain.GetGain();
double albumPeak = albumGain.GetPeak();

Calls are not thread safe, so if you're processing tracks in multiple threads, just synchronize on albumGain whenever you call AppendTrack.

Copyright (C) 2001-2009 David Robinson and Glen Sawyer
Improvements and optimizations added by Frank Klemm, and by Marcel M�ller.
Porting by Ivailo Karamanolev