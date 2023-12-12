import React, { useState } from 'react';

const articles = [
  {
    id: 1,
    title: 'Understanding the difference between grid-template and grid-auto',
    content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. ...',
  },

];

const HighlightedText = ({ text, highlight }) => {
  if (!highlight.trim()) {
    return <>{text}</>;
  }

  const parts = text.split(new RegExp(`(${highlight})`, 'gi'));
  return (
    <>
      {parts.map((part, i) =>
        part.toLowerCase() === highlight.toLowerCase() ? (
          <mark key={i}>{part}</mark>
        ) : (
          part
        )
      )}
    </>
  );
};

const SearchApp = () => {
  const [searchTerm, setSearchTerm] = useState('');
  const [searchResults, setSearchResults] = useState([]);

  const handleSearch = () => {
    const results = articles.filter((article) =>
      article.title.toLowerCase().includes(searchTerm.toLowerCase())
    );
    setSearchResults(results);
  };

  return (
    <div>
      <h1>Search:</h1>
      <input
        type="text"
        placeholder="Type keywords or phrases"
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
      />
      <button onClick={handleSearch}>Search</button>
      <p>{searchResults.length} posts were found</p>

      {searchResults.map((result) => (
        <div key={result.id}>
          <h2>
            <HighlightedText text={result.title} highlight={searchTerm} />
          </h2>
          <p>
            <HighlightedText text={result.content} highlight={searchTerm} />
          </p>
        </div>
      ))}
    </div>
  );
};

export default SearchApp;
