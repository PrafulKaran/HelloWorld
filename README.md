import { useState, useRef, useEffect } from 'react';
import { createPortal } from 'react-dom';

function RowWithMenu(props) {
  const [menuOpen, setMenuOpen] = useState(false);
  const [menuPosition, setMenuPosition] = useState({ x: 0, y: 0 });
  const menuRef = useRef(null);

  useEffect(() => {
    const handleClick = (e) => {
      if (menuRef.current && !menuRef.current.contains(e.target)) {
        setMenuOpen(false);
      }
    };

    document.addEventListener('mousedown', handleClick);

    return () => {
      document.removeEventListener('mousedown', handleClick);
    };
  }, [menuRef]);

  const handleContextMenu = (e) => {
    e.preventDefault();
    setMenuOpen(true);
    setMenuPosition({ x: e.clientX, y: e.clientY });
  };

  const handleCloseMenu = () => {
    setMenuOpen(false);
  };

  const handleMenuSelect = (menuItem) => {
    console.log(`Selected menu item: ${menuItem}`);
    setMenuOpen(false);
  };

  return (
    <div className="row-with-menu">
      <div onContextMenu={handleContextMenu}>
        {props.rowData.name}
      </div>

      {menuOpen && (
        <div
          className="context-menu"
          ref={menuRef}
          style={{
            position: 'absolute',
            top: menuPosition.y,
            left: menuPosition.x,
          }}
        >
          <ul>
            <li onClick={() => handleMenuSelect('Edit')}>Edit</li>
            <li onClick={() => handleMenuSelect('Delete')}>Delete</li>
          </ul>
        </div>
      )}
    </div>
  );
}

export default RowWithMenu;
