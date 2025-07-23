# music
MusicPlaylist
import React, { useState } from 'react';
const MusicPlayer = () => {
  const [playlist, setPlaylist] = useState([]);
  const [currentIndex, setCurrentIndex] = useState(null);
  const [newSong, setNewSong] = useState('');
  const addSong = () => {
    if (newSong.trim()) {
      setPlaylist([...playlist, newSong]);
      if (currentIndex === null) setCurrentIndex(0);
      setNewSong('');
    }
  };
  const nextSong = () => {
    if (playlist.length === 0) return;
    setCurrentIndex((currentIndex + 1) % playlist.length);
  };
  const prevSong = () => {
    if (playlist.length === 0) return;
    setCurrentIndex((currentIndex - 1 + playlist.length) % playlist.length);
  };
  const jumpToSong = (index) => {
    setCurrentIndex(index);
  };
  const removeSong = (index) => {
    const updatedPlaylist = playlist.filter((_, i) => i !== index);
    setPlaylist(updatedPlaylist);
    if (updatedPlaylist.length === 0) {
      setCurrentIndex(null);
    } else if (index === currentIndex) {
      setCurrentIndex(0);
    } else if (index < currentIndex) {
      setCurrentIndex(currentIndex - 1);
    }
  };
  return (
    <div style={{ padding: '20px', fontFamily: 'Arial' }}>
      <h2> Music Playlist</h2>
      <div>
        <input
          type="text"
          value={newSong}
          placeholder="Enter song title"
          onChange={(e) => setNewSong(e.target.value)}
        />
        <button onClick={addSong}>Add Song</button>
      </div>
      <h3>Playlist:</h3>
      <ul>
        {playlist.map((song, index) => (
          <li
            key={index}
            onClick={() => jumpToSong(index)}
            style={{
              cursor: 'pointer',
              fontWeight: index === currentIndex ? 'bold' : 'normal',
              color: index === currentIndex ? 'blue' : 'black',
            }}
          >
            {song}
            <button
              style={{ marginLeft: '10px', color: 'red' }}
              onClick={(e) => {
                e.stopPropagation();
                removeSong(index);
              }}
            >
              
            </button>
          </li>
        ))}
      </ul>
      <div>
        <button onClick={prevSong}> Previous</button>
        <button onClick={nextSong}> Next</button>
      </div>
      <h3>
        Current Song:{' '}
        {currentIndex !== null ? playlist[currentIndex] : 'No song selected'}
      </h3>
    </div>
  );
};
export default MusicPlayer;


